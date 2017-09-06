# When To Remove Feature Flags

It’s a good idea to keep a feature flag around for a sensible amount of time after it has been enabled for everyone. This allows us to have a "kill switch" for the feature if, somehow, something arises that just was not expected.

With that in mind, feature flags are technical debt and should not be long lived.

Once enabled for public release, a flag should be removed at some reasonable time afterwards, preferably within the same cycle. [Launch Darkly](https://app.launchdarkly.com), the service we use to manage feature flags, provides visual indicators that a flag has been rolled out to everyone and can be considered for removal.

  
To encourage remembering to clean up the old feature flags we suggest that you create a PR for removing the feature flag at the same time that you create the PR that introduces it. This has a couple of benefits:

1. You have the most context about what needs to be removed, and the code affected, at the point you’re creating the feature. This context only diminishes every day after you ship the feature
2. It doesn’t become someone else’s job to remove the feature flag for which they may have little or no context
3. It serves as a reminder for us to remove the feature flag when we see the PR in the list on github

  
There is obviously a small overhead in having to keep the PR rebased against master but we believe this is a small price to pay to keep our codebase relatively clean of stale feature flags.

## A Note On Flag Removal

One approach to remembering to remove a feature flag that we've had success with is the following:

1. At the point that you move something to public release, set a Slack reminder, for one week from now, to remind you to remove the flag
2. When Slack reminds you, ping James, Alicia and Gary to confirm they are confident in the feature and happy for the flag to be removed
3. Rebase your flag removal PR, give it a final test to ensure it works as expected and request a fellow engineer to review and merge
4. Once the PR change is deployed, delete the flag from the [Launch Darkly dashboard](https://app.launchdarkly.com/default/production/features).



