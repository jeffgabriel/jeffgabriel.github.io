---
title: Minimum Viable Features
layout: default
description: Understanding what MVP is and isn't and how it relates to feature growth.
copyright: copyright &copy; 2018 Jeff Gabriel
---
## {{page.title}}

I think pretty much everyone is familiar with the MVP concept in software. It's been around as an idea since 2001 and surged in popularity with Reis' *Lean Startup* in 2011. Plenty of time to enter the popular conscienciousness as a meme both in Dawkins' original sense and in the 'share pictures on social media' sense (thanks [Henrik Kniberg](https://twitter.com/henrikkniberg) for perhaps the most relatable pictogram).

![Henrik Knibergs popularized MVP pictogram](https://i.ytimg.com/vi/0P7nCmln7PM/hqdefault.jpg){:style="width:400px"}

As such, this idea of MVP has taken on many meanings and flavors and can be somewhat ambiguous when thrown around in a software development shop. I believe we're close to the original conception if we're discussing it as a way to enable a short feedback loop as an extension of learnings from iterative development. The whole point is learning. Importantly though - learning from actual end users. So in my opinion it's not MVP if

- It isn't viable.
- You're not delivering it to the actual end user.
- You can't or won't change anything based on delivering it.

When I think about what 'viable' is I think about delivering on the value proposition of the product. I work on a machine learning API. I think you would agree we missed the mark if we delivered an MVP by allowing you to upload data but not run any algorithms. Or to put it another way, you have to enable the core functionality; in my case, performing machine learning. Then there's the all important step of actually delivering to end users. It's just UAT if you're delivering it to your internal customer or your customer representative, or god forbid, your 'QA team'. This idea is central to me - you have to be able to deliver regularly to production or you just aren't capable of having MVPs (I'm not talking about continuous deployment; we'd have to open a whole new conversation to cover what that means). Of course that is tied to the 3rd requirement because if you can't deliver regularly to production you cannot change based on feedback. You could change your backlog or change your priorities, but you won't be able to change the product fast enough to iterate. That's the *can't*, but to finalize this section let's talk about when you *won't* change. 

In the Reis way of thinking about the MVP you're trying to figure out what your product should actually be in order to establish product-market fit. What delights the customer? What will they pay for? What will they tell their friends about? Part of this product journey is helping customers figure out what they want because they don't really know either. This is where the strong conceptual meaning of MVP starts to mix poorly with the actual ongoing implementation of a software product. If a viable product has been delivered and you're not going to pivot from that value proposition, then you're no longer iterating on MVP. You are now iterating on features - and perhaps actually just adding more of them. That is one form of *won't change*. 

The other is within feature development. If we look at the picture above we see at some point a move from scooter to bike. That's quite a change, and I think most of us work on features at scooter scale for a very long time before a bike emerges. So perhaps we need to talk about MVF (Features). You would then rightly accuse me of just making up terms to talk about *Sprints* or other agile development processes. But I will rejoinder and suggest that the principle which holds for features is the delivery and change process associated with feature growth. Often it's easy to talk about MVP repeatedly within a product that actually isn't changing its core deliverable. It's just as easy to talk about putting out an MVP of a feature when we have no intention of coming back to it. I think we often mean that we just need something out the door right now. We can have an agile development process to enable the feedback loop internally without delivering an MVF. We can also deliver quickly, but then move on to the next feature without having time to work in the customer's feedback on the previous feature. These things are fine and often totally necessary; but they are neither MVP or MVF.

I'll date myself and tell you that when I was in middle school (jr. high, or whatever you call it) I had a metal shop teacher, Mr. Preston <sup name="a1">[1](#f1){:target="_self"}</sup>. I don't remember his first name but I do remember the sign that hung in his shop:
<div style="font-size:1.3em"> 
> If you don't have time to do it right, when are you going to have time to do it over?
</div>
I always liked that quip, and the straightforward meaning is as a rhetorical question. But sometimes in software we have an answer. My point however in this post is that if you can't answer that question then you are not delivering an MVP(F). The reason you should care is that it's not nice to lie to yourself. If you, your team, your business unit, or your management is using the term 'MVP' without the re-work plan then you may just be piling up an insurmountable debt of poorly planned features.

The goal should always be honesty in these sitations. Maybe you're just doing iterative development internally without customer input? That's fine. But so far as what's going into production, if you're not going to come back to the feature then make sure you have taken the time to plan everything it **must** have as far as you know right now. That is now the release criteria and it's not an MVP. Share **that** vision of the product with your team. Don't sell the future state (or some notion of "lean-ness") and deliver the intermediate with no plan to come back.

<span style="font-size:.8em"><b id="f1">1</b> This guy was a real blacksmith that made nails and other things on an anvil while we worked on our projects. He was also old, cranky, and awesome. He once hung a kid on a hook by his belt because he wouldn't stop talking. Sure, that'd probably get you fired today, but it was a little bit awesome at the time. In his class you didn't just learn metal, you learned life.</span> [↩](#a1){:target="_self"}