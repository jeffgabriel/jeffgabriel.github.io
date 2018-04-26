---
title: Branching Out with Elm
layout: default
description: The value of taking technical risks and my experiences with Elm.
copyright: copyright &copy; 2018 Jeff Gabriel
---
## {{page.title}}

Yeah, I worked at that title for minute to get just the right level of dad-joke groaniness. I don't know too much about the Elm tree but it sounds like a plentiful and useful wood. My topic though is actually the [web application programming language elm](http://elm-lang.org/). I was only just introduced to elm at the beginning of the year; about 4 months ago. Fast-forward and now my team and I have completed a relatively complex [new web app](https://github.com/Nexosis/dashboard) that is the dashboard for our machine learning API.

<img src="https://www.ars.usda.gov/ARSUserFiles/oc/graphics/photos/jul96/k7310-2i.jpg" style="display:block;margin-left:auto;margin-right:auto" height="220" />

#### Out on a Limb
I was introduced to elm by our FP-loving teammate Zach, who was going to be tasked most directly with the dashboard project. This was an important new project for our company and it would have a relatively aggressive target date given the proposed scope. Of course when it was suggested that we should also put a new technology into the platform, my risk-averse side was on high alert. Yet, as I've noted before you have to hire smart people and then trust them. I also think it's important to be very careful about stifling innovation. My principles were running right into my fears. But we're not troglodytes listening to only our fears - principles must win out. 

I asked for a few examples of similarly complex sites already using elm and began to investigate the possibilities. Honestly, I didn't see what I was looking for. None of the examples were self-evidently mature or complex enough to reduce my fears. And yet, Zach was certain this would ultimately save us time. The primary point was that we wouldn't have to tangle with the usual javascript-based debugging headaches. He also suggested that the overall learning curve would be smaller than for something like React - and we were definitely going to need help from team members who didn't know any of the above (mostly me). I asked for a few assurances before we went ahead: Everyone who needs help gets help from Zach; Zach builds a baseline app to get us started; and once we're beyond the point of no return the team agrees to just dig in until problems are resolved. As an aside, it turned out that Zach was a very patient and helpful teacher. This was a good thing because this group of long time OOP developers struggled for a while with our first dive into functional programming. 

#### Don't Cut the Branch You're Standing On
Our direction was set and now we needed to tackle the learning curve. Again, the fact that elm is a functional language was probably the largest single hurdle for our team. Each developer needed to spend some time on tutorials and eduction sites to get oriented. Otherwise, the learning is all in knowing what's in the language. We found ourselves googling the simplest of concepts - knowing what we want to do, just not how to do it. Nothing elm-specific about that. Another difference was in the debugging. First of all, most of what you do is fight the compiler. The compiler can be extremely helpful because all of the code can be proved or disproved as correct. This helpfulness comes out as compiler errors. While it was a little difficult to read the errors at first, they're actually full of useful information and point to exactly what you did wrong. Fix the error, try again, repeat. If you get the thing to compile you're usually in great shape. It doesn't mean your app meets specifications of course - but it won't crash on you at runtime.  There are no null reference exceptions, no failures to parse a forgotten character, etc. As an elm developer you simply have to embrace the compiler, as it is your friend. Once running you then use the time-travelling debugger to watch the state changes. Again this was new territory for our team but once you embrace the functional paradigm it makes sense. All taken together I would say that the non-Zach team members were about 1/3 productive for the first two weeks, and ramped up from there over another 2 or 3 weeks. The key to making it was commitment. We were not turning back. However the language itself was really very slim and didn't make for too large a curve in the first place. One last comment on learning - use https://ellie-app.com/ a lot. Working out basic concepts and scenarios in isolation there was essential to my learning process.

#### Setting Down Roots
I better finish this soon or I'll run out of similies for the section headers...

<img src="https://upload.wikimedia.org/wikipedia/commons/4/4c/Port_Gamble%2C_WA_-_Camperdown_Elm_-_detail_of_trunk%2C_branch_structure.jpg" height="250" style="display:block;margin-left:auto;margin-right:auto;width:50%"/>

One of my concerns going in was around maturity. Would we be able to do everything we needed to do without major complications? It turned out that we were in good shape here. We have complicated charts and graphs in our application which couldn't be handled by existing elm-friendly implementations; we also did a couple of custom ports for local storage, XmlHttpRequest, and cookies. Otherwise we used what was available. I would say that we probably had to do a little extra lifting on creating common controls like pagers, etc. that you might find ready examples of in other frameworks. Yet, I ultimately prefer the simplicity of our elm application over the more involved javascript frameworks. 

It took a few extra hours from everyone on the team, but I believe we're all happy with our decision to use elm. We learned new things, built what was needed, and have provided an additional elm app to the community.  

- You can check out our dashboard code here: [https://github.com/Nexosis/dashboard](https://github.com/Nexosis/dashboard)
- The client to interact with the Nexosis Machine Learning API is here: [https://github.com/Nexosis/nexosisclient-elm](https://github.com/Nexosis/nexosisclient-elm)

---
<p><small>elm tree: https://www.ars.usda.gov/news-events/news/research-news/2011/hidden-elm-population-may-hold-genes-to-combat-dutch-elm-disease/</small></p>
<p><small>elm roots: By Byrnstar [CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0)], from Wikimedia Commons</small></p>