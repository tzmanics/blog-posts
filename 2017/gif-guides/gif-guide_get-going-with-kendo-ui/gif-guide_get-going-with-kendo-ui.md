# Gif Guide: Get Going with Kendo UI

Using [Kendo UI components in your Angular application](http://www.telerik.com/kendo-angular-ui/components/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack) helps you make a robust application quickly with succinct code. When you're working on a deadline, like during Angular Attack 😉😉, or just a regular stressful deadline, like getting work to a client on time, coding faster is better. Having succinct, easy-to-read code is great when you're working in a team or even just to future YOU. After all, you probably can't even remember what you had for lunch yesterday (me either) 🤷.

Okay, let's get going.

## Get Your Environment Ready

It is best to work with the latest stable version of Node & npm.

```bash
nvm install stable // to update to the latest stable version

// or if you want to keep you modules

nvm install stable --reinstall-packages-from=6.4.0
npm i npm -g // to update npm
```
![node & npm update](images/node-npm-update.gif)

## Get Your Project Created

From the directory where you want your project to live, use the Angular CLI to create a new project. First, install the [Angular CLI](https://github.com/angular/angular-cli).
![angular cli install](images/angular-cli.gif)

Then we just need to ask the CLI to create our new project and use the `-ng4` flag to make sure we're using version 4 of Angular (like all the cool kids 🤙).

```bash 
ng new ATTACK -ng4
```

![new angular project](images/ng-new.gif)

Ahhh, a fresh new project. To make sure everything is hunky dory 🤠, serve up the project and head to `http://localhost:4200/` to take a look.

```bash
ng serve
```
![Serve it up](images/ng-serve.gif)

In the words of Angular CLI contributor, [@Broco](https://twitter.com/brocco), BAM!

![a site is born](images/app-works.png)

### Get git...ing
Personally, I find that this is the perfect time to create a git repository and push the fresh project up.

```bash
cd ATTACK/ // move into your project directory
git init
git remote add origin <your repo\'s url>
```
![Get going with git](images/git-init.gif)

Add all the things, then push.

```bash
git status // check all the files that need added
git add . // 😱
git commit -m 'initial commit'
git push origin master
```

*I usually stay away from `git add .` because it can be dangerous but in this case we\'re only sending up the initial files so 👌*

![git add & push](images/git-add.gif)

Now we have a reference point to when all things were good 😇. I\'ll make a commit to this repo with every new step we take. Just look for the 🐙 to find the links to the new commits.

🐙 [initial commit](https://github.com/tzmanics/angular-attack/commit/d07d4fd49b8c641a510720cdbd2e1456a8e6f8ce)

## Get the Progress NPM Registry

### Get Access

If you haven\'t worked with Kendo UI components you will want to setup an account [HERE](https://www.telerik.com/login/v2/telerik?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack) in order to access our registry. All of our component modules are distributed NPM packages that live in our private registry but you just need your Progress Telerik account credentials to access them 👍.

Once you're setup we can login to the Progress registry.

```bash
npm login --registry=https://registry.npm.telerik.com/ --scope=@progress
```

If you get an error like this your credentials are not correct or you may not have activated your account. Check your email 📧 for an activation link.

![Login Error](images/login-error.gif)

Once you're all set you should have this lovely 'Logged in...' message to greet you 😍

![logged in](images/login.gif)

## Get the Chart Component

To use the Kendo UI components for your Angular project you will take the same steps, no matter which component you use:

- `npm install` the component's module
- import the module & import the component directive in your `module.ts` file
- & incorprate it into your template `html` file

Here we'll look at the chart 📊 component so we can also look at some data binding. You can check out all the available components [HERE](http://www.telerik.com/kendo-angular-ui/components/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack).

### Get the Module

First, you will want to install the module for our [chart component](http://www.telerik.com/kendo-angular-ui/components/charts/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack) and save it to your app's dependencies with the `-S` flag.

```bash
npm i -S @progress/kendo-angular-charts @progress/kendo-angular-intl @progress/kendo-drawing hammerjs
```
*you will see warnings like shown below but they are not detrimental to your project*

![installing the module](images/npm-i.gif)

### Get the Code in 👩‍💻

Inside your `app.module.ts` file you want to add the code to import the chart module, import the 'hammerjs' dependency and import the directive into your app module.

`src/app/app.module.ts`
```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';
import { ChartsModule } from '@progress/kendo-angular-charts';
import 'hammerjs';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    ChartsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
![add the code](images/module.gif)

If you're like me and like to be safe rather than sorry, feel free to run `ng serve` again to make sure your app is golden ☀️.

🐙 [install & import commit](https://github.com/tzmanics/angular-attack/commit/983f230eb1086e5026bcc395e98974efd408b59f)

### Get Styled
In order for your app to look awesome with very minimal effort you can add the [Kendo UI default theme](http://www.telerik.com/kendo-angular-ui/components/styling/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack). Again, you just need to install in with `npm i` then include it in your `.angular-cli.json` file.

```bash
npm install -S @progress/kendo-theme-default
```
![install the theme](images/npm-theme.gif)

For the fun part, we get to edit our `.angular-cli.json` file to include the theme 🎉.

`.angular-cli.json`
```json
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "project": {
    "name": "attack"
  },
  "apps": [
    {
      "root": "src",
      "outDir": "dist",
      "assets": [
        "assets",
        "favicon.ico"
      ],
      "index": "index.html",
      "main": "main.ts",
      "polyfills": "polyfills.ts",
      "test": "test.ts",
      "tsconfig": "tsconfig.app.json",
      "testTsconfig": "tsconfig.spec.json",
      "prefix": "app",
      "styles": [
        "../node_modules/@progress/kendo-theme-default/dist/all.css", // 💅
        "styles.css"
      ],
      "scripts": [],
      ...
```
![edit the cli config](images/cli-config.gif)

🐙 [get styled commit](https://github.com/tzmanics/angular-attack/commit/b9f9b7d6f9ba820cfadbeaa15ae8f6e43bd1622d)

### Get Data in There!

In the 'component.ts' file you can change your title and create some data to export.

`src/app/app.component.ts`
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'Winning App';
  private items: any[] = [{
    name: "puppies",
    data: [3, .65, 2, .50]
  },{
    name: "bunnies",
    data: [2, 1, .25, 3]
  },{
    name: "snakes",
    data: [1, .5, 1, .5]
  }];
```
![add data](images/add-data.gif)

🐙 [get data in there commit](https://github.com/tzmanics/angular-attack/commit/43cb0a48a7ace82ec9452cb6076bb765aa8cd879)

### Get a Chart

Now you can add the chart component to your template and bind the data created in the `component.ts` file. We'll keep the graph simple here because you still get a lot of interactions with just the basic graph but check out the [API](http://www.telerik.com/kendo-angular-ui/components/charts/api/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack) to see all the ways you can control & customize your chart.

First, the chart components `<kendo-chart>` and `<kendo-chart-series>` are added. Then, when you add the `<kendo-chart-series-item>` you can use `*ngFor` to loop through your list of items exported from `component.ts` and bind the items properties to the series item's name and data. For this chart we set the `type` to `area` to create an area graph, but there are a lot of options for series or graph types [in the Chart component docs](http://www.telerik.com/kendo-angular-ui/components/charts/chart/series-types/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack)!

`src/app/app.component.html`
```html
<h1>
  {{title}}
</h1>

<kendo-chart>
  <kendo-chart-series>
    <kendo-chart-series-item *ngFor="let item of items"
      type="area" [data]="item.data" [name]="item.name">
    </kendo-chart-series-item>
  </kendo-chart-series>
</kendo-chart>
```
![adding the chart code](images/add-chart.gif)

Now when you run `ng serve` you should find a beautiful, interactive chart!

![ze chart](images/final.gif)

Remember, you can always check in with the repo commits to see if your code changes match.

🐙 [get a chart commit](https://github.com/tzmanics/angular-attack/commit/a4fb2a03b1ac4d553bbfd63c26d86e212f596fb1)

That's all you need to get started with Kendo UI components & even put a chart in your app! Good luck with your app 👍 We're rooting for you 🙌

Resources:
- [Components Home Page](http://www.telerik.com/kendo-angular-ui/components/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack)
- [Charts Docs](http://www.telerik.com/kendo-angular-ui/components/charts/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack)
- [Charts API](http://www.telerik.com/kendo-angular-ui/components/charts/api/?utm_medium=website&utm_campaign=kendo-ui-angular-attack&utm_source=angular-attack)
- [Angular CLI Repo](https://github.com/angular/angular-cli)