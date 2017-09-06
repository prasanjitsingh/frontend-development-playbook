# Removing a Flag

After a sensible time has passed since your feature went to **Public Release**, it's time to remove the feature flag.



Firstly you should verify that all users are receiving the `true` variation of the feature flag. You can see this in the [Launch Darkly dashboard](https://app.launchdarkly.com/default/production/features). It looks like this:

![](/assets/flag-for-removal.png)

Notice the orange circle with an orange dot in the middle? 

Next, if you followed the [Feature Flagging Guidelines](/feature-flags/feature-flagging-guidelines.md), you should have a PR ready that removes the feature flag and associated code from the codebase. Ensure that the PR is rebased with the current `master` branch and have it reviewed by a fellow engineer. When it's good, merge and deploy it.

Finally, go back to Launch Darkly and delete the feature flag.

