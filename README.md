# kiss-vuex

[![](https://api.travis-ci.org/HalZhan/kiss-vuex.svg?branch=master)](https://travis-ci.org/HalZhan/kiss-vuex)
[![](https://img.shields.io/david/HalZhan/kiss-vuex.svg)](https://github.com/HalZhan/kiss-vuex)
[![](https://img.shields.io/david/dev/HalZhan/kiss-vuex.svg)](https://github.com/HalZhan/kiss-vuex)
[![](https://img.shields.io/github/license/HalZhan/kiss-vuex.svg)](https://github.com/HalZhan/kiss-vuex)

One powerful library for using vuex more easily followed KISS principle.

## Introduction

`kiss-vuex` support the easiest way to create vuex's store. It just exports one function named "Store" and you can use it like below:

    - [@Store](#@Store)
    - [Store](Store)

### @Store

As a decorator, you just need to add it above the class statement.

```js
import { Store } from 'kiss-vuex';

@Store
class AppStore {
    counter = 0;
    timeStamps = [];
    info = {
        counter: 0
    };
}

const appStore = new AppStore;

export {
    AppStore,
    appStore
}
```

> Note: You have to add decorator plugins to your babel.config.js or set compilerOptions.experimentalDecorators "true" in the tsconfig.json file.
>

**Use with babel**

You have to install such below development dependencies firstly.

```bash
$ npm i -D @babel/plugin-proposal-decorators @babel/plugin-proposal-class-properties
```

Then add such plugins to the `.babelrc.js` or `.babelrc` file.

```js
module.exports = {
    plugins: [
        ["@babel/plugin-proposal-decorators", { legacy: true }],
        ["@babel/plugin-proposal-class-properties", { loose: false }]
    ],
    presets: [
        [
            "@babel/env",
            {
                modules: false
            }
        ]
    ]
};
```

Import the store in the place you want to use it.

```js
import { appStore } from './appStore'
import Vue from 'vue';

export default Vue.component("app-opr", {
    computed: {
        counter() {
            return appStore.counter;
        },
        timeStamps() {
            return JSON.stringify(appStore.timeStamps);
        },
        timeInfo() {
            return JSON.stringify(appStore.info);
        }
    },
    template: `
  	<div>
        <strong>Operate Area</strong>
        <div><button @click="doClick()">Click me</button></div>
        <div>
    	<strong>Show Area</strong>
            <p>Click times: {{counter}}</p>
            <p>Timestamps: {{timeStamps}}</p>
            <p>timeInfo: {{timeInfo}}</p>
        </div>
    </div>
  `,
    methods: {
        doClick() {
            appStore.counter++;
            appStore.timeStamps.push(new Date());
            appStore.info.counter++;
            appStore.info[appStore.counter] = date.valueOf();
        }
    }
});
```

### Store

As a common function, you can just pass object to it.

```js
import { Store } from 'kiss-vuex';

const appStore = Store({
    counter = 0,
    timeStamps = []
});

export {
    appStore
}
```

Then you can import the store in the place you want to use it like above.

There are online examples you can take a look at.