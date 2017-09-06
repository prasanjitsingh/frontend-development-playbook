# Feature Flagging Guidelines



1. **No change is too small to be feature flagged**. Start with the mind set that a change will be feature flagged. If you choose not to, there should be considered reasoning behind why that’s the case
2. **Bugs generally do not require a feature flag**. But keep up communication with Growth and Support about their release lifecycle
3. **Feature flags are not just for hiding/showing something on the UI**. Ensure that a disabled feature flag short circuits any new logic that might otherwise run behind the scenes.
4. **Put thought in to what type of feature flag applies for your use case** and use the associated naming conventions. This helps to quickly identify what the intention of the feature flag is.
5. **Where you choose to place the feature flag, in code, matters**. Each feature is different and can bring with it different flagging needs. Put considered thought in to where the best place to put the feature flag "gate" is and strive to have easy to understand, and more importantly, follow, code paths that can be easily removed.
6. **Create a PR to remove the feature flag at the same time that you create the PR that introduces it**. It’s a small overhead that will save you further down the line. You never have more context about the change than you do when you're creating it



