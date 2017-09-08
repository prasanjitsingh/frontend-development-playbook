# Duplicate Imports Of Static Files

If you are in a situation where you need to make a change to a static file that is imported and used in the code, you'll find that you're probably not able to use the variation helper in that file. 

So, in a situation where you might be doing this:

```git
export default [
  'security.customer.authentication_type',
  'security.customer.social_authentication.twitter',
  'security.customer.social_authentication.facebook',
  'security.customer.social_authentication.google',
  'security.customer.sso.jwt.login_url',
  'security.customer.sso.jwt.logout_url',
- 'security.customer.sso.jwt.shared_secret'
- 'security.customer.sso.jwt.shared_secret',
+ 'security.customer.sso.jwt.service_name'
];
```



**Consider:**

```js
//app/lib/foo.js
export default [
  'security.customer.authentication_type',
  'security.customer.social_authentication.twitter',
  'security.customer.social_authentication.facebook',
  'security.customer.social_authentication.google',
  'security.customer.sso.jwt.login_url',
  'security.customer.sso.jwt.logout_url',
  'security.customer.sso.jwt.shared_secret'
  'security.customer.sso.jwt.shared_secret',
  'security.customer.sso.jwt.service_name'
];
```

```js
//app/lib/foo-old.js
export default [
  'security.customer.authentication_type',
  'security.customer.social_authentication.twitter',
  'security.customer.social_authentication.facebook',
  'security.customer.social_authentication.google',
  'security.customer.sso.jwt.login_url',
  'security.customer.sso.jwt.logout_url',
  'security.customer.sso.jwt.shared_secret'
  'security.customer.sso.jwt.shared_secret'
];
```

```js
import foo from 'app/lib/foo';
import fooOld from 'app/lib/foo-old';

// snip

things: computed(function() {
  if (!variation('feature-new-things')) {
    return fooOld;
  }
  
  return foo;
})
```







