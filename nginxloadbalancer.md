## Dynamic Nginx Proxy Registration
Due to some limitations in Azure's app gateway implementation I found myself putting an Nginx load balancer in front of an Azure Scale Set. Unfortunately, this presented a another problem in how I would let Nginx know that a new machine was added to or removed from the scale set. While the behavior I am about to describe can be implemented other ways - not least of which is just using Nginx Plus which does this out of the box - I think the problem is common enough to warrant a 'free' implementation. 
### Nginx Configuration
Nginx has a very simple configuration to load balance requests among many servers. The base setup is just like that of any proxy, but you include multiple hosts in the upstream server (per [the docs](http://nginx.org/en/docs/http/load_balancing.html)):
```conf
http {
    upstream myapp1 {
        server srv1.example.com;
        server srv2.example.com;
        server srv3.example.com;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://myapp1;
        }
    }
}
```
The issue in our situation of course is that we don't know those servers ahead of time. To solve this problem I need a server which comes online in the scale set to signal the nginx server and subsequently update the upstream configuration block with its dynamic ip address. I figured the best way to handle this was with a simple *curl* command in the startup script using the custom script extension for Linux. On the Nginx server side I decided the easiest way to stand up a simple REST endpoint would be with Node.js.

> A small aside about Node - I have had a hard time figuring out why Node at all from an application design perspective. Sharing code with the front end hasn't really been motivating, and server side languages and  frameworks abound. In this case Node seemed perfect - cross platform,  easy install, lightweight server.

In any case, you can take a look at the server itself in the [repo](https://github.com/Nexosis/nginxregistration/blob/master/registrationServer.js). I used the *nginx-conf* package to modify the configuration, and *restify* to expose RESTful endpoints to either add or remove servers from the configuration. The interface expects either an IP or name which can be reached from the Nginx server. If no configuration exists, then it will be started and when the last server is removed it will remove the upstream section.

### Wrapping Up
The final bit of the way this all works is that you need to reload Nginx config after it has been modified. For that I am using child_process. In our environment we have this deployed on Docker which creates an extra layer to work through and the implementation leaves a little work to do. In this version I'm restarting the whole container. With Nginx this is an extremely quick operation, but if you had multiple servers coming online at once it would be problematic.  The proper way to reload Nginx config is with a reload command which drains connections and then reloads. 
