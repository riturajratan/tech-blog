---
author: riturajratan
comments: true
date: 2019-09-08 21:36:48+00:00
layout: post
link: http://riturajratan.com/JavaScript
slug: lint-files-before-commit
title: Lint files before commit
categories:
- JavaScript
tags:
- JavaScript
- TypeScript
- EcmaScript
- hooks
---

Ya so after a long long time I am back :)

So most of the time, we have an issue that why our friends commit files with errors like

1. linting is not done .
2. without proper indentation.
3. and bla bla bla.

So for this we can set-up some hooks in git so when someone works on any files and tries to commit files then first he needs to resolve all errors after that he can commit files by this, code quality is also improved.

**Requirement :**

so for this we need to install 2 packages in our dev dependencies.

1. <a href="https://www.npmjs.com/package/husky" target="_blank"> Husky</a> (npm install husky --save-dev)
2. <a href="https://www.npmjs.com/package/lint-staged" target="_blank"> Husky</a> (npm install lint-staged  --save-dev) 

**Setup :**

So in our package.json file, we need to setup like below Here I am taking two configurations for `Tslint` and for `Eslint` As most of the time, we are working in angular.js and react.js ;). 
I am assuming my all files in the src folder 

### for TSlint

so for this we need to install additionally `tslint` package as it mention below in devDependencies

    {% highlight JSON %}
   {
  "name": "test tslint",
  "version": "0.0.0",
  "private": true,
  "dependencies": {
    //your dependencies
  },
  "devDependencies": {
    "husky": "^3.0.3",
    "lint-staged": "^9.2.1",
    "tslint": "^5.8.0"
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  }
  ,
  "lint-staged": {
    "{src}/**/*.{js,ts}": [
      "tslint -c tslint.json",
      "git add"
    ]
  }
}
{% endhighlight %}


### for ESlint
so for this we need to install additionally `eslint` package as it mention below in devDependencies
    {% highlight JSON %}
   {
     "name": "test tslint",
    "private": true,
   
    "dependencies": {
      //your dependencies
    },
    "devDependencies": {
        "husky": "^3.0.3",
        "lint-staged": "^9.2.1",
        "eslint": "^5.16.0",
    },
    "husky": {
        "hooks": {
            "pre-commit": "lint-staged"
        }
    },
    "lint-staged": {
        "**/{src,lib}/**/*.{js,jsx}": [
            "eslint --fix",
            "git add"
        ]
    }
}

{% endhighlight %}


##DEMO
[![so when you commit its look like below]({{ site.url }}/uploads/lint.gif)

SRC: taken from https://www.npmjs.com/package/lint-staged