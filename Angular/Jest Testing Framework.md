#tools 
# Definition
Jest is a browser less testing and runner framework that is now supported in Angular 16 [[Unit testing]].
Browser less testing will significantly improve runner performance thus reducing the waiting time making our development cycle faster.
Jest syntax is no different to Jasmine so we can migrate with ease.

# Usage
Update `test.builder` in `angular.json` (See more: [[Angular config#angular.json]])
``` json
{  
  "projects": {  
    "my-app": {  
      "architect": {  
        "test": {  
          "builder": "@angular-devkit/build-angular:jest",  
          "options": {  
            "tsConfig": "tsconfig.spec.json",  
            "polyfills": ["zone.js", "zone.js/testing"]  
          }  
        }  
      }  
    }  
  }  
}
```

# Browser testing
Quoted from [Moving to Jest and Web Test Runner](https://blog.angular.io/moving-angular-cli-to-jest-and-web-test-runner-ef85ef69ceca)

>Since Karma is also [now deprecated](https://github.com/karma-runner/karma), this is a good time to update our browser testing infrastructure as well. 

> We have been particularly impressed with [Web Test Runner](https://modern-web.dev/docs/test-runner/overview/), a browser-based unit test runner. It is developed by [Modern Web](https://modern-web.dev/blog/introducing-modern-web/), an organization dedicated to improving web tools to work _with_ modern browsers and technologies instead of against them. We think Web Test Runner would be a great addition to the Angular tooling ecosystem. **So we are also adding support for Web Test Runner in a future Angular release.** 