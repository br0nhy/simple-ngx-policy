<p align="center">
  <img height="256px" width="256px" style="text-align: center;" src="https://cdn.rawgit.com/jgololicic/simple-ngx-policy/master/demo/src/assets/logo.svg">
</p>

# simple-ngx-policy - Simple Angular 2+ statement &amp; resource management library

[![npm version](https://badge.fury.io/js/simple-ngx-policy.svg)](https://badge.fury.io/js/simple-ngx-policy),
[![Build Status](https://travis-ci.org/jgololicic/simple-ngx-policy.svg?branch=master)](https://travis-ci.org/jgololicic/simple-ngx-policy)
[![Coverage Status](https://coveralls.io/repos/github/jgololicic/simple-ngx-policy/badge.svg?branch=master)](https://coveralls.io/github/jgololicic/simple-ngx-policy?branch=master)
[![dependency Status](https://david-dm.org/jgololicic/simple-ngx-policy/status.svg)](https://david-dm.org/jgololicic/simple-ngx-policy)
[![devDependency Status](https://david-dm.org/jgololicic/simple-ngx-policy/dev-status.svg?branch=master)](https://david-dm.org/jgololicic/simple-ngx-policy#info=devDependencies)
[![Greenkeeper Badge](https://badges.greenkeeper.io/jgololicic/simple-ngx-policy.svg)](https://greenkeeper.io/)

## Demo

View all the directives in action at https://jgololicic.github.io/simple-ngx-policy

## Dependencies
* [Angular](https://angular.io) (*requires* Angular 2 or higher, tested with 2.0.0)

## Installation
Install above dependencies via *npm*. 

Now install `simple-ngx-policy` via:
```shell
npm install --save simple-ngx-policy
```

---
##### SystemJS
>**Note**:If you are using `SystemJS`, you should adjust your configuration to point to the UMD bundle.
In your systemjs config file, `map` needs to tell the System loader where to look for `simple-ngx-policy`:
```js
map: {
  'simple-ngx-policy': 'node_modules/simple-ngx-policy/bundles/simple-ngx-policy.umd.js',
}
```
---

Once installed you need to import the main module:
```js
import { SnpModule } from 'simple-ngx-policy';
```
The only remaining part is to list the imported module in your application module. The exact method will be slightly
different for the root (top-level) module for which you should end up with the code similar to (notice ` SnpModule .forRoot()`):
```js
import { SnpModule } from 'simple-ngx-policy';

@NgModule({
  declarations: [AppComponent, ...],
  imports: [SnpModule.forRoot(), ...],  
  bootstrap: [AppComponent]
})
export class AppModule {
}
```

Other modules in your application can simply import ` SnpModule `:

```js
import { SnpModule } from 'simple-ngx-policy';

@NgModule({
  declarations: [OtherComponent, ...],
  imports: [SnpModule, ...], 
})
export class OtherModule {
}
```

## Behaviour (output of tests):
```
  Resource.class
    ✔ parses default parameter into namespace/module/resource
    ✔ parses provided string parameter into namespace/module/resource
    ✔ parses only first three chunks of provided resource string into namespace/module/resource
    ✔ parses provided "namespace:module:" string parameter into namespace/module/resource
    ✔ parses provided "namespace::" string parameter into namespace/module/resource
    ✔ parses provided "::" string parameter into namespace/module/resource
    ✔ parses provided "::employees" string parameter into namespace/module/resource
    ✔ parses provided ":human-resources:employees" string parameter into namespace/module/resource
  SnpStatement.class
    ✔ parses default parameter into module/component/action/ statement members
    ✔ parses provided parameter into module/component/action/ statement members
    ✔ parses provided "one chunk string" parameter into module/component/action/ statement members
    ✔ parses provided "two chunk string" parameter into module/component/action/ statement members
    ✔ parses provided "three chunk string" parameter into module/component/action/ statement members
    ✔ parses provided "one chunk and a colon string" parameter into module/component/action/ statement members
    ✔ parses provided "one chunk and two colons string" parameter into module/component/action/ statement members
    ✔ parses provided "three chunk and two colons string" parameter into module/component/action/ statement members
    ✔ parses provided "two colons and a chunk string" parameter into module/component/action/ statement members
    ✔ parses provided "one colon and two chunks string" parameter into module/component/action/ statement members
  SnpPolicyService
    Has 'providePolicy' static method which
      ✔ Provides 'empty' SnpPolicy when called with no parameters
      ✔ Uses default config 'defaultPolicyConstraint' when no constraint is specified in SnpModule.forRoot(config: SnpConfig)
      ✔ Accepts constraint and provides a policy with given constraint
      ✔ Provides SnpStatement and SnpResource from parameter strings
    Has 'canAccess' static method which compares SnpPolicy against a list of SnpPolicies[]
      When SnpModules' 'defaultPolicyConstraint' is configured to 'ALLOW' (default)
        ✔ Returns TRUE for 'empty' policy and 'empty list'
        ✔ Returns FALSE for 'empty' policy and 'empty list' when policies' constraint is DISALLOW
        ✔ Returns TRUE for 'empty' policy and 'empty list' when policies' constraint is ALLOWED
        ✔ Returns TRUE for empty 'policy' when list is provided (not empty)
        ✔ Returns FALSE for empty 'policy' with constraints set to DISALLOW when list is provided (not empty)
        ✔ Returns TRUE for empty 'policy' with constraints set to ALLOWED when list is provided (not empty)
        ✔ Returns TRUE if the policy is not in the list
        ✔ Returns FALSE if the policy with constraint DISALLOW is not in the list
        ✔ Returns TRUE if the policy's statement is on the list AND policy's resources match
        ✔ Returns TRUE if the policy's statement is on the list AND policy's resources match AND policy's constraint is DISALLOW
        ✔ Returns TRUE if the policy's statement is on the list AND policy's resources match AND policy's constraint is ALLOWED
        ✔ Returns FALSE if the policy's statement is on the list BUT resources does not match
        ✔ Returns FALSE if the policy's statement is on the list BUT resources does not match and policy's constraint is DISALLOW
        ✔ Returns FALSE if the policy's statement is on the list BUT resources does not match and policy's constraint is ALLOWED
      When SnpModule 'defaultPolicyConstraint' is configured to 'DISALLOW' (provided in SnpModule.forRoot(config: SnpConfig))
        ✔ Returns FALSE for 'empty' policy when list is not provided
        ✔ Returns TRUE for 'empty' policy with constraints ALLOW when list is not provided
        ✔ Returns FALSE for empty policy when list is provided (not empty)
        ✔ Returns TRUE for empty with constraint ALLOWED policy when list is provided (not empty)
        ✔ Returns FALSE if policy is not in the list
        ✔ Returns TRUE if policy with constraint ALLOW is not in the list
        ✔ Returns TRUE if policy's statement is on the list AND policy's resources match
        ✔ Returns TRUE if policy's statement is on the list AND policy's resources match AND policy's constraints is DISALLOW 
        ✔ Returns FALSE if the policy's statement is on the list BUT resources does not match
        ✔ Returns FALSE if the policy's statement is on the list BUT resources does not match AND policy's constraint is ALLOWED
  SnpPolicy.module
    ✔ has default configuration
```


## License

Copyright (c) 2017 jgololicic. Licensed under the MIT License (MIT)

