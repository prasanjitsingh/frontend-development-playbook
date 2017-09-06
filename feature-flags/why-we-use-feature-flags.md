# Why we use feature flags

We prefer to ship code as often as possible. This helps avoid long running branches of work and helps focus us on shipping small, quality pieces of code that do one thing well.  


Feature flags help us achieve this goal in that we are able to merge and deploy code to production without making it accessible to users and to then incrementally roll out the functionality as and when we see fit.  


The ability to do this serves a number of purposes, such as, but not limited to:  


1. Ability to merge code, for features that are not fully finished, in to `master` early to ensure we don’t have long running branches
2. Ability to QA features internally before releasing to customers to ensure they are bug free
3. Ability to beta test features with external customers to ensure they solve the problems we originally predicted they would 

Feature flags also allow us to coordinate with the Growth and Support teams before features reach customers. This becomes increasingly more important as our applications grow because Support need to be aware and educated on the features they are ultimately supporting and Growth need to be aware of what we are shipping so they can market features correctly to our existing and potential customers.



By achieving the things above we put ourselves in a position to ship high quality features, more often, with a very high confidence that they will solve our customers’ problems well.



