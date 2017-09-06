# When To Use Feature Flags

## tl;dr;

**Always**.



However, things are never that black and white. But the point is that we should be approaching everything with the intention to feature flag it, and only after considered thought and reasoning should we decide not to feature flag something.



> Approach everything with the intention of wrapping it in a feature flag. Only after considered thought and reasoning should we decide otherwise.

  
No feature is to small to be wrapped in a feature flag. The size of the change is not what matters. It’s about being able to control the rollout of the change that is important. It’s about communication of the change with people such as those in the Growth and Support teams who need to be aware of what is released and when. By feature flagging changes, we give Growth and Support the responsibility to decide when to release the features and to whom.



## What about bug fixes?

Bug fixes are often an exception to the rule above. This is because a bug is a defect in our code. A bug fix is correcting something that we should have done correctly the first time round. We, therefore, almost always want to roll out the fix to everyone, as soon as we can. There is no point holding back a fix for a bug from people and so, a feature flag usually is not appropriate.

  
This, however, does not mean that, because there is no feature flag for Growth and Support to enable, that we should skip the communication with them about the fix going out. In fact, it’s even more important that we do so.

It’s likely support are the ones that have requested the fix so it’s imperative that we continue to communicate with Growth and Support as we would any other feature. Just let them know that the fix will be available as soon as it’s deployed.

