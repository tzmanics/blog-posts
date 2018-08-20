# Creating Robust React Applications with Kendo UI

Hi, I'm Tara Z. Manicsic, [@tzmanics](https://twitter.com/tzmanics) on Twitter, and I'm a developer advocate for [Progress](https://www.progress.com). I’m here today to walk you through creating a robust application in React with [Kendo UI's library built from the ground up specifically for React](https://www.telerik.com/kendo-react-ui). If you're wondering what Kendo UI is, you can check out the [first post]() in this series and all the [accompanying videos](https://www.youtube.com/watch?v=3goM9S5vFDo&list=PLLGlTD7u3kMo1TKLmFShXMhP-fIculjOu). You can also find the repo that follows this project commit to commit [here](https://github.com/tzmanics/kendoui-react-video-series). Without further ado, let's jump into the code to build out this project.

The first thing that we're going to do today is use [`create-react-app`](https://github.com/facebook/create-react-app) to create our react application. Then, we will find the components that we're going to use on the [Kendo UI website](https://www.telerik.com/kendo-react-ui/components), and install them  using npm. Finally, we will also install a theme, the [Kendo UI default theme](https://www.telerik.com/kendo-react-ui/components/styling/theme-default/). We'll talk a little more about themes as we get to that section. So let's jump into the code.

We first build out the project using [`create-react-app`](https://github.com/facebook/create-react-app). It is a open source project, coming from Facebook, and it gives you a skeleton of a react application. To build the app we go to our terminal and globally install `create-react-app`, using npm and the `-g` flag to make it globally accessible. Once installed we can run `create-react-app` along with the project name.

```
npm create-react-app -g
create-react-app awesome-app
```

We now have the basic `README.md`, a `node_modules` folder, `package.json` and `public` and `src` directory. Today we'll mostly be working in the `src` directory. I want to go ahead and give you a look at what this looks like so far. So we'll run `npm start` and `create-react-app` has set it up so the app will reload on save. Magic ✨.

*insert image*

Next, just to get everything ready for us to create this project, we'll start installing our Kendo UI components. Remember you can always refer to the [Kendo UI documentation](https://www.telerik.com/kendo-react-ui/components/) to get more information about all the components. For this project we'll be working with [`Buttons`](https://www.telerik.com/kendo-react-ui/components/buttons/), [`DropDowns`](https://www.telerik.com/kendo-react-ui/components/dropdowns/), [`NumericTextBox`](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/), and [`Grid`](https://www.telerik.com/kendo-react-ui/components/grid/) components. First off, we'll go ahead and install all of those now. If we take a look at `Buttons` first, we see that in the documentation we have an 'Installation' section that let's us know how to get started.

*insert image*

We just need to install the `Buttons` library with npm by running:

`npm install @progress/kendo-react-buttons`

We can dismiss the `--save` or `-S`, flags because with NPM 5.x and greater, modules are saved by default. Nice, so we have a button now!

That's is basically how you install all the components: `npm i @progress/kendo-react-<componennt-name>`. That is how we would install `DropDowns` and `NumericTextBox`. The only difference is that we would also want to install the [`internationalization` package](https://www.telerik.com/kendo-react-ui/components/globalization/i18n/) to take advantage of the globalization features for the Kendo UI components. I would show you how to install these separately BUT since we are also using the `Graph` component we won't need to. This is because there is so much you can do with the Graph you tend to install all these when you use the Graph. So, technically you can install all these things at once.

`npm install @progress/kendo-react-grid @progress/kendo-data-query @progress/kendo-react-inputs @progress/kendo-react-intl @progress/kendo-react-dropdowns @progress/kendo-react-dateinputs @progress/kendo-react-pdf @progress/kendo-drawing`

Okay, that was quick. Now we can go ahead and talk about the theme. If you saw the video before this, you know that I really like the idea of installing [these themes](https://www.telerik.com/kendo-react-ui/components/styling/), because you don't have to do any CSS work if you don't want to. For this project, we actually won't be doing any customization in CSS, because we'll solely rely on the styling from the styling libraries. One of the tools that I want to show you that I think is fantastic, is the [Progress Theme Builder](https://themebuilder.telerik.com/). This builder lets you customize your theme for the Kendo UI components. You can base it off of Material, Bootstrap or your own custom settings. For today, we are actually going to install the default theme. In the next post I'll show you how to import that into our project. For right now, all we are going to do is run:

`npm install @progress/kendo-theme-default`

If you take a look at your project's `package.json` file in the main directory, all the libraries we installed will be listed under `"dependencies"`.

In this post, we have prepared ourselves by installings all the awesome components that we need to create a robust application in react using the Kendo UI library that is built from the ground up specifically for React. Please remember if you have any questions at all, ping us on Twitter [@KendoUI](https://twitter.com/kendoui), or me personally [@tzmanics](https://twitter.com/tzmanics). Check out the rest of this series in [video](https://www.youtube.com/playlist?list=PLLGlTD7u3kMo1TKLmFShXMhP-fIculjOu) or [blog post]() form to continue on the journey of building this application. Hopefully, we will see you soon!