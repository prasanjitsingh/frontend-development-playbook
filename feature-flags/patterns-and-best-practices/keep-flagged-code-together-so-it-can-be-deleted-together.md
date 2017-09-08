# Keep Flagged Code Together So It Can Be Deleted Together

Try and keep the overhead of mentally parsing feature flag logic to a minimum. This makes it as easy as possible for the reader of the code to understand the control flow that will be taken when the flag is enabled/disabled. This also makes it easier to delete feature flag code later on and gives a nicer, and easier to grok, git diff when doing so.

**Instead of:**

```js
.then(() => {
  if (variation('push-notifications')) {
    return this.get('realtimePush').registerUserDevice();
  }

  return true;
})
```

To remove this feature flag we would need to delete lines `2`, `4` and `6` and then outdent line `3`. This can cause extra mental overhead when trying to ensure the logic hasn’t changed when removing the feature flag, not to mention complicates the git diff for the person reviewing the code.



**Consider:**

```js
.then(() => {
  if (!variation('push-notifications')) {
    return true;
  }

  return this.get('realtimePush').registerUserDevice();
})
```

To remove this feature flag would simply need to delete lines `2`-`4`. It’s much easier to grok the and remove gating logic between the two code paths.

