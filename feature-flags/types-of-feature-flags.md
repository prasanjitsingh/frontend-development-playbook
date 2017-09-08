# Types Of Feature Flags

A flag is a flag is a flag right? Well, not necessarily.

In our experience we’ve found that feature flags can have different uses and intentions at different times depending on the context of the change they are wrapping. They can also have different life cycles. Based on this, we have settled upon the following types of feature flags that we use in our codebase:

## Feature flags

_Prefix:_ `feature-`

_Expected Lifespan_: **short/medium**

Used to incrementally enable a feature to users until such point that it’s rolled out to everyone.

Depending on the size of the feature and the level of testing it requires, these flags may live for a short time or a longer period of time. But the goal is always to eventually remove them and the old code they replaced \(if relevant\).

A piece of work that is behind a `feature-` flag should generally be in a state that it could be turned on for users at any time. This means one should not use this type of flag to hide work that is in progress or incomplete.

## Operations flags

_Prefix:_ `ops-`

_Expected Lifespan_: **short**

Used to wrap operational aspects of the code. These flags might wrap code that enables extra instrumentation of code or changes that have unclear performance implications and therefore may need to be disabled in production quickly if needed.

Refactoring should be flagged with an `ops-`  flag.

These flags should be relatively short lived and removed once confidence is gained in the code change, however, it may not be uncommon to have a small number of longer lived "kill switches" around code that needs to be turned off at short notice.

## Plan flags

_Prefix:_ `plan-`

_Expected Lifespan_: **long/permanent**

Used to override what is dictated by the user’s plan. If the user’s plan says a given feature is disabled, we can use a plan flag to enable it on a selective basis. These deal with *established* features, rather than pre-release changes.

This comes in useful if, for example, you would like to demonstrate an established feature to a customer on their own instance without requiring them to upgrade or otherwise change plan.

Another example is if a particular user’s plan configuration listed a feature as disabled unexpectedly. In this case we could use a plan flag to enable it until we can ascertain the cause of the problem on the backend.

These flags are typically long-lived and may be permanent. They should be removed if we find they are simply never enabled.
