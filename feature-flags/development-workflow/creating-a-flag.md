# Creating a Flag

Firstly, you need a [Launch Darkly](https://app.launchdarkly.com/) account. If you do not have one, ask one of your fellow engineers to set you up.

## Create The Flag

Once you have an account, you need to manually create the feature flag in Launch Darkly. To do this, head to the [Launch Darkly dashboard](https://app.launchdarkly.com/default/production/features) and click the "New" button:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_FCFB6B7F3CB376C52A81D6F874DA2104BF2448A223BE547F4F73AED7BCAA2D00_1504263775385_image.png)

Then you need to enter the feature flag details:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_FCFB6B7F3CB376C52A81D6F874DA2104BF2448A223BE547F4F73AED7BCAA2D00_1504265996136_image.png)

A few things to note here are:

1. Decide on what type of feature flag you are creating. See the [Types Of Feature Flags](/feature-flags/types-of-feature-flags.md) section for more information on this.

2. Prefix the "Name" with the type of flag it is, eg, `[Feature]` . This makes it much easier to differentiate the flag types when scanning through the list of all flags. \(This can be changed after creation\)

3. Enter the "Key" for which you will refer to the flag in your application code. Please ensure it is prefixed correctly, eg features are prefixed with `feature-`. \(This cannot be changed once created\)

4. "Description" is obviously optional but providing this will help Growth to understand what a feature flag is used for

5. For the "flag type" we've traditionally been only using Boolean type flags \(they are either on or off\) however it’s possible to use multivariate flags as well, although these would typically be used for A/B testing different variations of a solution. You’ll likely be reaching for Boolean types.

6. I can’t imagine we’ll use many \(or any\) permanent flags. Checking this will mean that LD won’t prompt us to remove the flag even if it’s been rolled out to all users for some time

7. Make sure your flag is available for the client-side SDK. It will be by default so you shouldn’t need to touch this option



## Setup The Flag

Once you’ve saved the flag you’ll want to ensure it’s disabled by default:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_FCFB6B7F3CB376C52A81D6F874DA2104BF2448A223BE547F4F73AED7BCAA2D00_1504268854272_image.png)

A few things to note here are:

1. The "Targeting" switch specifies whether the flag is turned on or not. Basically it’s a kill switch. When targeting is off, the value mentioned at the bottom of this image will be served, in this case, `false`
2. The "Default rule" represents the value that will be served for this flag when it is turned on and a user does not match the rules specified for this flag \(or there are no rules specified as in this example\)
3. Feel free to turn the targeting on now so you don't need to circle back to do so later

At this point the feature flag has been created in Launch Darkly and disabled by default.



## A Side Note

Upon creation of a new feature flag, Launch Darkly sends a webhook to Slack which will create a post in the \#product-feature-flags channel. This post allows Growth and Support to be informed that a new feature was indeed created, gives them a link to it in Launch Darkly, and allows them to coordinate the lifecycle of that feature flag, through the [Feature Release Stages](https://kayako.gitbooks.io/feature-delivery-playbook/content/feature-release-stages.html).

The Slack post looks like this:

![](/assets/import.png)

