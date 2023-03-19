---
{"dg-publish":true,"permalink":"/feature-toggles/feature-toggles-by-martin-fowler/","tags":["feature-toggles"]}
---


links: [[feature-toggles/feature toggles MOC\|feature toggles MOC]] ,[Feature Toggles (aka Feature Flags)](https://martinfowler.com/articles/feature-toggles.html)


Please summarise the text block using only outline.

{if you want to add other information like libraries, documentation, etc}
Considerations:

{PUT CONSIDERATIONS HERE}

{/if}

{
_Feature Toggles (often also refered to as Feature Flags) are a powerful technique, allowing teams to modify system behavior without changing code. They fall into various usage categories, and it's important to take that categorization into account when implementing and managing toggles. Toggles introduce complexity. We can keep that complexity in check by using smart toggle implementation practices and appropriate tools to manage our toggle configuration, but we should also aim to constrain the number of toggles in our system._


"Feature Toggling" is a set of patterns which can help a team to deliver new functionality to users rapidly but safely. In this article on Feature Toggling we'll start off with a short story showing some typical scenarios where Feature Toggles are helpful. Then we'll dig into the details, covering specific patterns and practices which will help a team succeed with Feature Toggles.

Feature Toggles are also refered to as Feature Flags, Feature Bits, or Feature Flippers. These are all synonyms for the same set of techniques. Throughout this article I'll use feature toggles and feature flags interchangebly.

## A Toggling Tale

Picture the scene. You're on one of several teams working on a sophisticated town planning simulation game. Your team is responsible for the core simulation engine. You have been tasked with increasing the efficiency of the Spline Reticulation algorithm. You know this will require a fairly large overhaul of the implementation which will take several weeks. Meanwhile other members of your team will need to continue some ongoing work on related areas of the codebase.

You want to avoid branching for this work if at all possible, based on previous painful experiences of merging long-lived branches in the past. Instead, you decide that the entire team will continue to work on trunk, but the developers working on the Spline Reticulation improvements will use a Feature Toggle to prevent their work from impacting the rest of the team or destabilizing the codebase.

### The birth of a Feature Flag

Here's the first change introduced by the pair working on the algorithm:

before

```
  function reticulateSplines(){
    // current implementation lives here
  }
```

these examples all use JavaScript ES2015

after

```
  function reticulateSplines(){
    var useNewAlgorithm = false;
    // useNewAlgorithm = true; // UNCOMMENT IF YOU ARE WORKING ON THE NEW SR ALGORITHM
  
    if( useNewAlgorithm ){
      return enhancedSplineReticulation();
    }else{
      return oldFashionedSplineReticulation();
    }
  }
  
  function oldFashionedSplineReticulation(){
    // current implementation lives here
  }
  
  function enhancedSplineReticulation(){
    // TODO: implement better SR algorithm
  }
```

The pair have moved the current algorithm implementation into an `oldFashionedSplineReticulation` function, and turned `reticulateSplines` into a **Toggle Point**. Now if someone is working on the new algorithm they can enable the "use new Algorithm" **Feature** by uncommenting the `useNewAlgorithm = true` line.

### Making a flag dynamic

A few hours pass and the pair are ready to run their new algorithm through some of the simulation engine's integration tests. They also want to exercise the old algorithm in the same integration test run. They'll need to be able to enable or disable the Feature dynamically, which means it's time to move on from the clunky mechanism of commenting or uncommenting that `useNewAlgorithm = true` line:

```
function reticulateSplines(){
  if( featureIsEnabled("use-new-SR-algorithm") ){
    return enhancedSplineReticulation();
  }else{
    return oldFashionedSplineReticulation();
  }
}

```

We've now introduced a `featureIsEnabled` function, a **Toggle Router** which can be used to dynamically control which codepath is live. There are many ways to implement a Toggle Router, varying from a simple in-memory store to a highly sophisticated distributed system with a fancy UI. For now we'll start with a very simple system:

```
function createToggleRouter(featureConfig){
  return {
    setFeature(featureName,isEnabled){
      featureConfig[featureName] = isEnabled;
    },
    featureIsEnabled(featureName){
      return featureConfig[featureName];
    }
  };
}

```

note that we're using ES2015's [method shorthand](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Method_definitions)

We can create a new toggle router based on some default configuration - perhaps read in from a config file - but we can also dynamically toggle a feature on or off. This allows automated tests to verify both sides of a toggled feature:

```
describe( 'spline reticulation', function(){
  let toggleRouter;
  let simulationEngine;

  beforeEach(function(){
    toggleRouter = createToggleRouter();
    simulationEngine = createSimulationEngine({toggleRouter:toggleRouter});
  });

  it('works correctly with old algorithm', function(){
    // Given
    toggleRouter.setFeature("use-new-SR-algorithm",false);

    // When
    const result = simulationEngine.doSomethingWhichInvolvesSplineReticulation();

    // Then
    verifySplineReticulation(result);
  });

  it('works correctly with new algorithm', function(){
    // Given
    toggleRouter.setFeature("use-new-SR-algorithm",true);

    // When
    const result = simulationEngine.doSomethingWhichInvolvesSplineReticulation();

    // Then
    verifySplineReticulation(result);
  });
});

```

### Getting ready to release

More time passes and the team believe their new algorithm is feature-complete. To confirm this they have been modifying their higher-level automated tests so that they exercise the system both with the feature off and with it on. The team also wants to do some manual exploratory testing to ensure everything works as expected - Spline Reticulation is a critical part of the system's behavior, after all.

To perform manual testing of a feature which hasn't yet been verified as ready for general use we need to be able to have the feature Off for our general user base in production but be able to turn it On for internal users. There are a lot of different approaches to achieve this goal:

-   Have the Toggle Router make decisions based on a **Toggle Configuration**, and make that configuration environment-specific. Only turn the new feature on in a pre-production environment.
-   Allow Toggle Configuration to be modified at runtime via some form of admin UI. Use that admin UI to turn the new feature on a test environment.
-   Teach the Toggle Router how to make dynamic, per-request toggling decisions. These decisions take **Toggle Context** into account, for example by looking for a special cookie or HTTP header. Usually Toggle Context is used as a proxy for identifying the user making the request.

(We'll be digging into these approaches in more detail later on, so don't worry if some of these concepts are new to you.)

![](https://martinfowler.com/articles/feature-toggles.htmlfeature-toggles/overview-diagram.png)

The team decides to go with a per-request Toggle Router since it gives them a lot of flexibility. The team particularly appreciate that this will allow them to test their new algorithm without needing a separate testing environment. Instead they can simply turn the algorithm on in their production environment but only for internal users (as detected via a special cookie). The team can now turn that cookie on for themselves and verify that the new feature performs as expected.

### Canary releasing

The new Spline Reticulation algorithm is looking good based on the exploratory testing done so far. However since it's such a critical part of the game's simulation engine there remains some reluctance to turn this feature on for all users. The team decide to use their Feature Flag infrastructure to perform a [**Canary Release**](https://martinfowler.com/bliki/CanaryRelease.html), only turning the new feature on for a small percentage of their total userbase - a "canary" cohort.

The team enhance the Toggle Router by teaching it the concept of user cohorts - groups of users who consistently experience a feature as always being On or Off. A cohort of canary users is created via a random sampling of 1% of the user base - perhaps using a modulo of user ID. This canary cohort will consistently have the feature turned on, while the other 99% of the user base remain using the old algorithm. Key business metrics (user engagement, total revenue earned, etc) are monitored for both groups to gain confidence that the new algorithm does not negatively impact user behavior. Once the team are confident that the new feature has no ill effects they modify their Toggle Configuration to turn it on for the entire user base.

### A/B testing

The team's product manager learns about this approach and is quite excited. She suggests that the team use a similar mechanism to perform some A/B testing. There's been a long-running debate as to whether modifying the crime rate algorithm to take pollution levels into account would increase or decrease the game's playability. They now have the ability to settle the debate using data. They plan to roll out a cheap implementation which captures the essence of the idea, controlled with a Feature Flag. They will turn the feature on for a reasonably large cohort of users, then study how those users behave compared to a "control" cohort. This approach will allow the team to resolve contentious product debates based on data, rather than [HiPPOs](http://www.forbes.com/sites/derosetichy/2013/04/15/what-happens-when-a-hippo-runs-your-company/).

This brief scenario is intended to illustrate both the basic concept of Feature Toggling but also to highlight how many different applications this core capability can have. Now that we've seen some examples of those applications let's dig a little deeper. We'll explore different categories of toggles and see what makes them different. We'll cover how to write maintainable toggle code, and finally share practices to avoid some of pitfalls of a feature-toggled system.

## Categories of toggles

We've seen the fundamental facility provided by Feature Toggles - being able to ship alternative codepaths within one deployable unit and choose between them at runtime. The scenarios above also show that this facility can be used in various ways in various contexts. It can be tempting to lump all feature toggles into the same bucket, but this is a dangerous path. The design forces at play for different categories of toggles are quite different and managing them all in the same way can lead to pain down the road.

Feature toggles can be categorized across two major dimensions: how long the feature toggle will live and how dynamic the toggling decision must be. There are other factors to consider - who will manage the feature toggle, for example - but I consider longevity and dynamism to be two big factors which can help guide how to manage toggles.

Let's consider various categories of toggle through the lens of these two dimensions and see where they fit.

### Release Toggles

Release Toggles allow incomplete and un-tested codepaths to be shipped to production as latent code which may never be turned on.

These are feature flags used to enable trunk-based development for teams practicing Continuous Delivery. They allow in-progress features to be checked into a shared integration branch (e.g. master or trunk) while still allowing that branch to be deployed to production at any time. Release Toggles allow incomplete and un-tested codepaths to be shipped to production as [latent code](http://www.infoq.com/news/2009/08/enabling-lrm) which may never be turned on.

Product Managers may also use a product-centric version of this same approach to prevent half-complete product features from being exposed to their end users. For example, the product manager of an ecommerce site might not want to let users see a new Estimated Shipping Date feature which only works for one of the site's shipping partners, preferring to wait until that feature has been implemented for all shipping partners. Product Managers may have other reasons for not wanting to expose features even if they are fully implemented and tested. Feature release might be being coordinated with a marketing campaign, for example. Using Release Toggles in this way is the most common way to implement the Continuous Delivery principle of "separating \[feature\] release from \[code\] deployment."

![](https://martinfowler.com/articles/feature-toggles.htmlfeature-toggles/chart-1.png)

Release Toggles are transitionary by nature. They should generally not stick around much longer than a week or two, although product-centric toggles may need to remain in place for a longer period. The toggling decision for a Release Toggle is typically very static. Every toggling decision for a given release version will be the same, and changing that toggling decision by rolling out a new release with a toggle configuration change is usually perfectly acceptable.
}





<hr class="__chatgpt_plugin">

role::assistant

# Feature Toggling

- Feature Toggles are a set of patterns to modify system behavior without changing code.
- Teams can use toggles for rapid and safe delivery of new functionality.
- Toggle categories include release, ops, experiment, permission, and experimental UI flags.
- Smart toggle implementation practices and appropriate tools help manage toggle complexity.
- Use feature toggles interchangeably with feature flags or bits.
- A toggle point is where the current implementation moves into an old function. 
- The `useNewAlgorithm` variable controls whether the new algorithm runs or not in the example given. 
- A toggle router allows dynamic control of which code path is live based on features enabled or disabled. 
- Various approaches allow testing a feature before releasing it to production users such as per-request routing or canary releases. 
    - Per-request routing uses special cookies while canary releases turn on features for only a small percentage of users at first.  
    - Using cohorts helps test how different user groups behave when exposed to new features compared to those who aren't exposed yet (control group).
    - A/B testing is also possible using similar mechanisms by turning on/off certain features for specific cohorts then comparing results between them
        - This approach resolves contentious product debates based on data rather than opinions from higher-ups (HiPPOs).
  - Release toggles enable trunk-based development allowing incomplete/untested codepaths shipped to production as latent code that may never be turned on.
  - Release toggles are transitionary by nature and should generally not stick around much longer than a week or two.

## Categories of Toggles

Toggles fall under these categories: 

1) **Release** – used in Continuous Delivery practice; incomplete/ untested codepaths shipped to prod as latent codes that may never be turned on.

2) **Ops** – used mainly by operations teams; enables runtime modification of infrastructure configuration items.

3) **Experimentation** – used for running experiments like A/B tests among others.

4) **Permission** – restricts access rights within applications; useful in multi-user environments like SaaS products.

5) **Experimental UI Flags** – exposes early-stage work-in-progress interfaces so developers get feedback quickly

<hr class="__chatgpt_plugin">

role::user


