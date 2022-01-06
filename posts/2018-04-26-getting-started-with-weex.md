---
title: Getting started with Weex
slug: getting-started-with-weex
date_published: 2018-04-26T13:25:11.000Z
date_updated: 2018-04-26T13:25:57.000Z
tags: vue, typescript, weex, javascript
excerpt: Creating Weex mobile apps using VueJS
---

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQI87l9CSPUicLWGxpFoqc3hQ41UbWcZO9_1NPx0-i0Bhxx100-vg)

## 1. Installation

With Yarn

    yarn global add --ignore-engines weex-toolkit
    

## 2. Create App

    weex create my-first-app
    

I chose -

- Babel stage-0
- Unit Tests : Yes
- EsLint: Yes
- Vue-Router: Yes
- WebRenderer: 1.0.x

    cd my-first-app
    npm install
    

*Note: Phantom JS will be downloaded to handle web rendering preview and Unit Tests. If you disable unit tests, PhantomJS is not used (Maybe we can try to use headless chrome instead)*

You'll see following output

    Success! Created first-weex-app at /Users/championswimmer/Development/Personal/Weex/first-weex-app
    
    Inside that directory, you can run several commands:
    
    
      npm start
      Starts the development server for you to preview your weex page on browser
      You can also scan the QR code using weex playground to preview weex page on native
    
      npm run dev
      Open the code compilation task in watch mode
    
      npm run ios
      (Mac only, requires Xcode)
      Starts the development server and loads your app in an iOS simulator
    
      npm run android
      (Requires Android build tools)
      Starts the development server and loads your app on a connected Android device or emulator
    
      npm run pack:ios
      (Mac only, requires Xcode)
      Packaging ios project into ipa package
    
      npm run pack:android
      (Requires Android build tools)
      Packaging android project into apk package
    
      npm run pack:web
      Packaging html5 project into `web/build` folder
    
      npm run test
      Starts the test runner
    

## 3. Add Platforms

You should have XCode, CocoaPods for iOS

You should have SDK and Emulator for Android

    weex platform add ios
    weex platform add android
    

## 4. Run Platforms

    weex run ios
    

or

    npm run ios
    

Same for Android

## 5. Add Typescript support

Reference [https://my.oschina.net/zaaksam/blog/1572320](https://my.oschina.net/zaaksam/blog/1572320)

    npm install -D typescript vue-property-decorator ts-loader@3
    

*NOTE: ts-loader v3 is needed as we use Webpack v3*

*src/types/vue-sfc.d.ts*

    declare module "*.vue" {  
      import Vue from 'vue'  
      export default Vue  
    }
    

*src/types/weex.d.ts*

    declare namespace we {  
      interface instance {  
      /** This variable contains all environmental information for the current Weex page */  
      config: any  
      
      /** Get all methods of a native module */  
      requireModule(name: string): any  
      }  
    }  
      
    declare var weex: we.instance
    

Add a tsconfig.json (**inside src folder**)

    {
      "compilerOptions": {
        "target": "es5",
        "lib": [
          "dom",
          "es5",
          "es2015"
        ],
        "typeRoots": ["types"],
        "module": "es2015",
        "moduleResolution": "node",
        "experimentalDecorators": true,
        "emitDecoratorMetadata": true,
        "removeComments": true,
        "suppressImplicitAnyIndexErrors": true,
        "allowSyntheticDefaultImports": true,
        "strict": true
      }
    }
    
    

#### Changes in webpack

*Note: Only highlighting portions to change*

    const weexEntry = {  
      'index': helper.root('entry.ts')  
    }
    .
    .
    .
    .
    entry: Object.assign(webEntry, {  
      'vendor': [path.resolve('node_modules/phantom-limb/index.ts')]  
    }),
    resolve: {
    	extensions: ['.ts', '.js', '.vue', '.json'],
    }
    

#### Change entry.js to entry.ts

    /* global Vue */  
      
    /* weex initialized here, please do not move this line */  
    import * as router from './router'  
    import App from '@/index.vue'  
    import Vue from 'vue'  
      
    new Vue({  
      el: '#root',  
      router,  
      render: h => h(App)  
    })  
    router.push('/')
    

In webpack.config.js and in config.js change `entry.js` mentions to `entry.ts`

---

> Written with [StackEdit](https://stackedit.io/).
