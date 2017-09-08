# Patterns And Best Practices

There are no black and white rules when it comes to what and how to feature flag code but there are some common patterns that start to emerge after a while.

The following is a collection of suggestions, patterns, advice and rules of thumb that we’ve compiled from our experiences with feature flagging code changes. These are not hard and fast rules however, through experience, we have found that these rules of thumb help us to keep our code and flags easy to read, maintain and remove.

If you find yourself wondering how to approach a particular implementation of a flag, see if any of the patterns below help.

* [Ensure enabled flags enable new functionality](/feature-flags/patterns-and-best-practices/ensure-enabled-flags-enable-new-functionality.md)
* [Avoid mixing flag condition logic with other logic](/feature-flags/patterns-and-best-practices/avoid-mixing-flag-condition-logic-with-other-logic.md)
* [Keep flagged code together so it can be deleted together](/feature-flags/patterns-and-best-practices/keep-flagged-code-together-so-it-can-be-deleted-together.md)
* [When changing the API of components, duplicate them](/feature-flags/patterns-and-best-practices/when-changing-the-api-of-components-duplicate-them.md)
* [When duplicating components, respect the original component name](/feature-flags/patterns-and-best-practices/when-duplicating-components-respect-the-original-component-name.md)
* Duplicate CP’s when dependent keys change based on feature flags



