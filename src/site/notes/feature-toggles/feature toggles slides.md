---
{"dg-publish":true,"permalink":"/feature-toggles/feature-toggles-slides/","tags":["feature-toggles"]}
---


links:: [[feature-toggles/feature toggles MOC\|feature toggles MOC]]

# Feature Toggles Slides

## Agenda

- Introduction
- How feature flags work
- Benefits of feature flags
- Categories of toggles
- Implementation techniques
- Toggle configuration
- Best Practices for using feature flags
- Testing feature toggles
- Potential drawbacks of feature flags 
- Conclusion

## Definition

> [!NOTE] Feature toggles/flags
> Software development technique that allows developers to turn on or off certain features or functionalities of an application without changing the codebase

safer and more frequent deployments

facilitate testing 

gathering feedback on new features

release new features to a small group of users 

test different variations of a feature

manage technical debt

easier to maintain and update an application over time

## Why Feature Toggles?

Conditional statement

```js
if ( featureFlagEnabled) {

  // execute code for feature

} else {

  // execute default code

}
```

## How Feature Flags Work

Toggle configuration control

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev3.png|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev3.png)

Source: https://martinfowler.com

- Canary releases / Product testing
- Dark launching
- Blue-green deployments
- Migrations
- System outage

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev5.jpg|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev5.jpg)

## Benefits of Feature Flags

Source: https://www.atlassian.com/continuous-delivery/principles/feature-flags

- Safer and more frequent deployments
- Controlled rollout of new features
- Testing and gathering feedback

## Categories of Toggles

- Release Toggles
- Experiment Toggles
- Ops Toggles
- Permissioning Toggles
  

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev11.png|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev11.png)

Source: https://martinfowler.com

>… enable trunk-based development for teams practicing Continuous Delivery. They allow in-progress features to be checked into a shared integration branch (e.g. master or trunk) while still allowing that branch to be deployed to production at any time. 

>

>Release Toggles allow incomplete and un-tested codepaths to be shipped to production as latent code which may never be turned on.

Source: https://martinfowler.com

Release toggles 

- No longer than a week or two
- Typically very static

Source: https://martinfowler.com

## Implementation Techniques

- De-coupling decision points from decision logic
- Inversion of Decision
- Avoiding conditionals

Source: https://martinfowler.com 

## Toggle Configuration

Source control and re-deployments 

Hardcoded Toggle Configuration

Parameterized Toggle Configuration (via command-line arguments or environment variables)

Toggle Configuration File

- Dynamic configuration
- Distributed toggle configuration
- Configuration services (Harness)
- Azure App Configuration

## Tools: Azure App Configuration

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev18.png|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev18.png)

Source: https://learn.microsoft.com/en-us/azure/azure-app-configuration/

Azure App Configuration provides a service to centrally manage application settings and feature flags.

Enables staged rollout of features for targeted audiences

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev20.png|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev20.png)

The feature flag is always enabled for user test@contoso.com, because test@contoso.com is listed in the Users section.

The feature flag is enabled for 50% of other users in the contoso.com group, because contoso.com is listed in the Groups section with a Percentage of 50.

The feature is always disabled for all other users, because the Default percentage is set to 0.

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev23.gif](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev23.gif)

## Best Practices for Using Feature Flags

- Clear naming conventions
- Regular maintenance and cleanup
- Monitoring and logging

## Testing Feature Toggles

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev25.png|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev25.png)

Testing without feature toggles

Exploratory testing

```
Test E1
Test E2
…
Test En
```

Regression testing 

```
Test R1
Test R2
…
Test Rn
```

Testing with feature toggles

Number of toggles N=2

Number of combinations C=4

|  | Toggle 1 | Toggle 2 |
| :-: | :-: | :-: |
| Combination 1 | ON | ON |
| Combination 2 | OFF | OFF |
| Combination 3 | ON | OFF |
| Combination 4 | OFF | ON |

Test each combination?

```
Test E1 – It is safe to skip it 
Test E2 – It is hard do decide. Is it safe to skip it?
Test E3 – We should test this.
...
Test En
```

Exploratory testing 

Regression testing 

```
Test R1 - It is safe to skip it 
Test R2 - It is hard do decide. Is it safe to skip it?
Test R3 – We should test this. 
…
Test Rn
```

Testing with feature toggles

- Number of toggles N=16
- Number of combinations C=65,536

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev30.jpg|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev30.jpg)

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev33.jpg|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev33.jpg)

Integration, E2E testing of large number of flags

![WYWM_2023_Presentation_Feature_Toggles_Maksim Zinovev35.jpg|500](/img/user/feature-toggles/img/WYWM_2023_Presentation_Feature_Toggles_Maksim%20Zinovev35.jpg)

Source: https://launchdarkly.com/blog/testing-with-feature-flags/

How do we test this? 

- Option 1:  

  - Test all combinations. Good luck :)

  - Minimal risk of missing bugs.

- Option 2:  
  - Assess all combinations and select only “realistic” ones which are likely to occur in the future. Test them.  
  - Accept the risk of “unknown”.
  - This will most likely require a lot of time and effort.  
- Option 3: 
  - Follow recommendation from the book. Use the current production configuration plus: 3 combinations (see next slide).
  - Accept the risk of “unknown”.
  - This will require less time and effort compared to option 1

Static, Boolean and release toggles

Use the current production configuration plus: 

1. Any toggles you intend to release set to ON
2. Any toggles you intend to release set to OFF
3. All toggles set to ON

Source: https://martinfowler.com

Testing of large number of flags (option 3)

![feature toggles slides-1679811617350.jpeg](/img/user/feature-toggles/attachments/feature%20toggles%20slides-1679811617350.jpeg)

Other strategies

1. Dynamic toggle: test users who move into or out of the targeted group
2. Experiment toggle: test consistency across user sessions, to ensure individual users are given the correct version at every login.
3. Permission toggle: explore toggle combinations to see how the new configuration interacts with existing option

## Potential Drawbacks of Feature Flags

- Increased complexity and technical debt
- Risk of feature flag fatigue
- Overreliance on feature flags

## Conclusion

- Feature flags are a powerful tool
- Follow best practices
- Testing will likely require more time and effort and understanding of context
- Will have to accept risks of “unknown” (not tested combinations)

## References

- [https://martinfowler.com/articles/feature-toggles.htm](https://martinfowler.com/articles/feature-toggles.htm)
- [https://martinfowler.com/bliki/CanaryRelease.html](https://martinfowler.com/bliki/CanaryRelease.html)
- [http://swreflections.blogspot.com/2014/08/feature-toggles-are-one-of-worst-kinds.html](http://swreflections.blogspot.com/2014/08/feature-toggles-are-one-of-worst-kinds.html)
- [https://www.abhishek-tiwari.com/decoupling-deployment-and-release-feature-toggles/](https://www.abhishek-tiwari.com/decoupling-deployment-and-release-feature-toggles/)[https://launchdarkly.com/blog/testing-with-feature-flags/](https://launchdarkly.com/blog/testing-with-feature-flags/)
- [https://dougseven.com/2014/04/17/knightmare-a-devops-cautionary-tale/](https://dougseven.com/2014/04/17/knightmare-a-devops-cautionary-tale/)
- [https://learn.microsoft.com/en-us/azure/azure-app-configuration/](https://learn.microsoft.com/en-us/azure/azure-app-configuration/)
- https://www.atlassian.com/continuous-delivery/principles/feature-flags



