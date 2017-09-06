# Enabling/Disabling a Flag

In general, engineers will have no need to enable feature flags as this is done by the Growth and Support teams. However, this doesn't mean that once a change has been merged in to `master` and deployed to production your job is finished.

Once a feature has been merged in to `master`, it is the engineer's job to follow and push that feature all the way through to **Public Release**. This means being receptive to changes and bugs that arise for the feature and coordinating with Growth and Support to move the feature through **Internal Release** to **Public Release**.

For more info on this release lifecycle of a feature, refer to the [Feature Delivery Playbook](https://kayako.gitbooks.io/feature-delivery-playbook/content/feature-release-stages.html).



## A Side Note

It isn't strictly true that engineers will not be enabling/disabling feature flags. There should be no need to enable/disable `feature-` feature flags for sure, as these enable user/customer facing features. However, as per the [Types of Feature Flags](/feature-flags/types-of-feature-flags.md) chapter, we may be implementing `ops-` based flags which enable/disable underlying code infrastructure type changes. These changes generally add no visible value to our customers and therefore aren't really the concern of the Growth and Support teams. These flags matter to engineers and we need to control and monitor when they are turned on and off. Therefore, `ops-` based feature flags are the exception to the rule where as an engineer, you will be in control of enabling and disabling the flag.



