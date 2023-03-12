---
{"dg-publish":true,"permalink":"/feature-toggles/configuration-flags-a-love-story-article/","tags":["feature-toggles"]}
---


links: [[feature-toggles/feature toggles MOC\|feature toggles MOC]]

# Configuration Flags: A Love Story

[Share URL](https://well.tc/SEu "Copy this URL and Share")

#feature-toggless  
  

Imagine sending code to production that does not execute—at least not in a way visible to the customer. When the time comes, the company changes a text file (called a configuration file), which does not require a new build or production push; that also makes rollback easier. Many companies, from big ones like Google and Amazon to smaller ones like Flickr and Etsy, credit dark releases with speeding time to market and reducing risk. Configuration flag (config flag) architecture also contributes to the capability to perform large-scale beta testing; for example, it contributes to the capability to perform multivariate testing at scale.

The problem is not the what, but the how; the actual implementation of config flags may well be the least-understood part of the continuous delivery stack. I’m not aware of a place to go to get what people need—a little training and advice on a straightforward way to build a config flag architecture in the [simplest way that can reasonably be expected to work.](http://c2.com/xp/DoTheSimplestThingThatCouldPossiblyWork.html)

In this article, I’d like to impart that training with some battle-tested strategies to implement and leverage config flags in production.

**Branch in Code, Not in Source Control  
**[As Paul Hammond has explained,](http://www.paulhammond.org/2010/06/trunk/alwaysshiptrunk.pdf) branching in source control (including Git) has limitations that make it an inappropriate strategy for managing production deployments.

[To quote Theo Schlossnagle](http://omniti.com/seeds/online-application-deployment-reducing-risk):

In the online world, a software product drives a service to which users have access. There is, most often, a single copy of the actual software product in use. There is one consumer of the software: you. The users are consumers of the service built atop the software.[](https://www.stickyminds.com/article/configuration-flags-love-story?page=0,1#_msocom_1)

In the online world, a software product drives a service to which users have access. There is, most often, a single copy of the actual software product in use. There is one consumer of the software: you. The users are consumers of the service built atop the software.

This is a key concept and I found it counter-intuitive the first few (hundred) times I heard it. So I’ll reiterate: the only deployed “copy” of my website is the one running in my data center. Many people may consume my _product._ But that product is a _service_ produced by the _single copy of my software_ that is running on the host(s) in my data center(s).

Once I had gotten used to viewing the problem this way, it is became obvious that I could make changes to the _product_ without affecting the quality of its _service._

**The Repo Doesn’t Have to Mirror the Org Chart  
**With config flags in place it’s possible for different groups to work on various projects at varying speeds, all while releasing weekly (or daily) to production.

Because each feature’s config flags are separate, it’s possible to deploy a feature to production while many other teams are arbitrarily working on other, much larger features in the same codebase.

Keep in mind, any code wrapped in a config flag is ready to go to production at any time. If it isn’t ready, the config flag is turned off and the result is a no-op. If the config flag is turned on but the code misbehaves, the config flag can be toggled off by changing a single line in the config file.

Therefore _anyone can release dark code at any time_ without affecting the behavior of the site or the progress of other projects within the same codebase. This single structural shift all but eliminates the need to develop new features on separate code branches.

With config flags, almost all new development can occur on the main branch. In other words, everyone can commit to trunk all the time, without anyone stepping on anyone else’s changes.

While everyone committing to trunk takes a couple of weeks to get used to, in the mid-to-long-term it represents a serious competitive advantage. Just [ask Google,](https://twitter.com/hogfish/status/344567813345779712) where 15,000 engineers commit to a single trunk and over 50 percent of the codebase changes every _week._ Facebook, Amazon, Netflix, Etsy, and IMVU all have similarly rapid commit cycles.

**Organization of The Config Flags  
**I want to start with an in-memory array that I define in a single source file somewhere in version control. This approach allows the team to scale to around a dozen deployments a _day_ before those limitations become a hindrance. (Most of the teams I work with find a dozen deploys of the same code base a day a limitation, but that’s another article.)

Putting the whole config in One Big Array™ means that there is one _source of truth_ for configuration. Anyone who wants an audit trail for configuration changes can get one by running git log on the config file. This simplicity is invaluable, especially with a team working to learn all the different elements on continuous delivery while delivering now code. This is yet another reason why it makes sense to get up-and-running with simple config flags right away, rather than trying to perfect the architecture first and holding off implementation until later.

With this in place, the team can write code and use conditionals (“if statements”) to determine which branch of code to execute—the new feature or not.

**How I Learned to Stop Worrying and Love the Config Flag  
**People frequently ask me, “Won’t my code be ugly once it is littered with conditionals?” I tell them, “Yes. But you’ll come to appreciate it.”

Branching in code isn’t any less complex than branching in source control. The config flag strategy enables me to _handle_ certain types of complexity in a better way.

It took a while for me to adjust after I was first introduced to this admittedly radical design pattern. At first the proliferation of config flags felt like a code smell.

Debugging branching in code is also easier than debugging version control for changes. To get a sense of what I’m saying here, think about the last time you debugged an _if_ statement. Now think about the last time you had to debug a _Git merge conflict;_ it’s orders-of-magnitude less difficult to coordinate.

**Config Flags in the Wild  
**In time, config flags come to define the architecture of any rapidly moving, continuously deployed product. Let me explain.

When thinking about config flags it’s _useful_ to confuse the idea of branch-by-abstraction with the idea of A/B split testing (also called multivariate testing).

In the context of an AB framework, a “config flag” is just a _variable_ that has a _boolean_ value. In the context of an AB framework, other “config flags” might have more complex settings, such as “display only to 1 percent of users” or “display only to users who opted in to the v2 Beta.”

Developing every feature around an AB framework enables me to experiment easily. It creates an ideal environment for releasing and iterating on [MVPs.](http://en.wikipedia.org/wiki/Minimum_viable_product) So an AB framework is a larger context to also consider when talking about how to best leverage config flags.

In practice, the use of partial rollouts and config flags can provide powerful capabilities. For instance, such an approach [has enabled Google to deploy the recent addition of a leap-second](http://googleblog.blogspot.com/2011/09/time-technology-and-leaping-seconds.html) to all of its system clocks simultaneously and seamlessly.

**Distinguishing between “Prod Config Flags” and “Dev Config Flags”  
**I find it useful to define an informal distinction between “production flags” and “dev flags.” Production flags being those “3:00 a.m. flags” that are meant to control the behavior of site features at a high level (eg: disable ratings-and-reviews) and dev flags being…everything else.

Usually dev flags are first used in the course of deploying unfinished code to production. The first test of a new dev flag’s functionality is when I verify that the under-development code “behind” the flag is not in fact executing (or having side effects) in production.

Over time, some of the flags I created at the inception of a feature will grow in importance and become its prod config flags. But most dev flags will be useful for a certain period of time and then eventually I will remove the old dev config flags.

In fact, the need to remove old config flag logic is another good reason to differentiate between dev and production flags. Old production flags will have to be removed very carefully (if ever). But for a released feature, removing dev config flags is mostly a matter of search-and-replace.

So not every config flag is meant to be toggled at 3:00 a.m..

**Who Are The Users of My Config Flags?  
**Since config flags are a _feature,_ I try to periodically ask the question “Who are the users of these config flags I’m creating?”

The first obvious answer is: Ops.

Above all others the system operations team will benefit from the ability to quickly disable problematic services. For instance, if a new ratings-and-reviews feature becomes computationally expensive for unknown reasons soon after release (and of course, my team finds this out at 3:00 a.m.) then the ops person on-call can mitigate the immediate problem by _deploying a single config flag_ that turns off ratings-and-reviews, thereby expediently removing the immediate problem of impending system overload.

The second important group of users is… me—the developer building the system. A config flag architecture (coupled with proper monitoring) supports my ability to experimentally and incrementally grow new features in production.

**Start Simple, Stay Simple  
**The practices outlined above are relatively easy to implement, given an environment where it is not too difficult for dev and ops teams to interact and cooperate.

By implementing config flags as part of initial development, engineers imbue all new features with the capability to leverage system-level strategies, such as multivariate testing, beta testing, and “emergency toggles” in which Ops can disable expensive systems before they result in cascading failures. This reduces the risk of the project, allowing testers to move from a “get-it-right” attitude (which is impossible) to instead say “we have enough information to ship this, at which point we’ll gain more information for little risk.”

<hr class="__chatgpt_plugin">

role::user

Please summarise the above text using only outline.

Condition 1: Use 1-2 sentences maximum for each point. 

Condition 2: List main points. Do not write as a paragraph.

Condition 3: Use indentation structure no more than 2 levels.

<hr class="__chatgpt_plugin">

role::assistant

- Implementing config flags can speed up time to market and reduce risk.
- Branching in code, not in source control, is a better strategy for managing production deployments.
- Config flags enable different groups to work on various projects at varying speeds, while releasing weekly or daily to production.
- The organization of config flags should be in a single source file somewhere in version control.
- Config flags in practice come to define the architecture of any rapidly moving, continuously deployed product.
- Distinguishing between “Prod Config Flags” and “Dev Config Flags” is useful.
- The users of config flags are Ops and the developers building the system.
- Start simple and stay simple.

<hr class="__chatgpt_plugin">

role::user
