# Adding a Kendo UI Grid, Dropdown List and More to React
Hi everyone. Tara Z. Manicsic here, [@tzmanics](https://twitter.com/kendoui) on Twitter. I’m a developer advocate for [Progress](https://www.progress.com/) working on the Kendo UI team. You've joined me here today in a series that we're creating to help you build a robust React application with the [Kendo UI library that was built specifically for React](https://www.telerik.com/kendo-react-ui). This is actually the third installment. In the [first post]() we talked about Kendo UI. With the [second post]() we installed everything we needed for this application, and created a React application with [`create-react-app`](https://github.com/facebook/create-react-app). But worry not, all the posts are listed below, as well as the [repo for building this project](https://github.com/tzmanics/kendoui-react-video-series) broken down into commits with all the code changes to help you along the way.

We're going to jump in today by bringing components into our React project. I want to show you a little bit about the components that we're going to be using today. First of all, we're going to be making a place where users can add a healthy goal and check how many iterations they want to do of that healthy habit. Then, we will be creating a grid that contains information, nutritional information, about fruits and vegetables.

Let's look at the components that we're going to be using today. For this post, we’ll just be bringing the components into our project. We'll be customizing them in the next post. There's a ton of documentation about these components and APIs that are very useful as well, and you find them here [Kendo UI’s React component pages](https://www.telerik.com/kendo-react-ui/components/grid/). Today we're building out our app with a [Grid](https://www.telerik.com/kendo-react-ui/components/grid/),  [DropDowns](https://www.telerik.com/kendo-react-ui/components/dropdowns/), a [NumericTextBox](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/) and a [Button](https://www.telerik.com/kendo-react-ui/components/buttons/). Who doesn't love a good button?

We will be starting out with the grid. You will see what we can do with the grid in the [customization post](), next in the series. Again, today we're just bringing it in, but there's so much that you can do with the `Grid` component that it could have its own series in itself. Let's jump into the code. As a refresher, we used `create-react-app` to create the application, then ran `npm start` in the background so that we could see the updates as we write our code. Today, we’ll start in the root directory, open the `src` directory and build out the `App.js` file. It’s not best practice to do all the work in the `App.js` file, but, for today, it keeps everything very clear for this tutorial. As you progress with these projects, it's highly recommended that you break everything into correct components and organize them in directories. For today, let's keep it simple, right?

Inside of our `App.js` file, we're going to start by importing all of the components that we need. While we're in here, let's actually delete the things we don't need. We don't need `logo.svg` and we don't need anything inside of the `App` div. Since we do not need this logo we will delete it from `src/logo.svg`. We will first import the `DropDownList` by importing it from `@progress/kendo-react-dropdowns`. Next, we will be using `NumericTextBox` from inputs. Finally, we'll be using the `Grid`. Also from the `Grid` library we will be using the `GridColumn`. Instead of having to write `GridColumn` every single time, we're just going to import it as `Column` to make it simpler. Now that we have all of our components imported we also need to install the theme we installed in the last post. One other thing that we need today is information, data for our grid to make it look super nice and filled with smart things. My favorite kind of application to make is one that I need, one that I can use. So I decided to grab some nutritional information about fruits and vegetables to put inside of our `Grid`. I put the info into a  JSON file inside of our `src` directory. Let me show you what that looks like.

*src/nutrition.json*
```json
[
 {
   "NDB_NO": 9427,
   "Description": "Abiyuch, raw",
   "Weight(g)": 114,
   "Measure": "0.5 cup",
   "Protein(g)Per Measure": 1.71,
   "Carbohydrate, by difference(g)Per Measure": 20.06,
   "Sugars, total(g)Per Measure": "9.75"
 },
 {
   "NDB_NO": 9002,
   "Description": "Acerola juice, raw",
   "Weight(g)": 242,
   "Measure": "1.0 cup",
   "Protein(g)Per Measure": 0.97,
   "Carbohydrate, by difference(g)Per Measure": 11.62,
   "Sugars, total(g)Per Measure": "10.89"
 },
...
{
   "NDB_NO": 11991,
   "Description": "Yautia (tannier), raw",
   "Weight(g)": 135,
   "Measure": "1.0 cup, sliced",
   "Protein(g)Per Measure": 1.97,
   "Carbohydrate, by difference(g)Per Measure": 31.9,
   "Sugars, total(g)Per Measure": "--"
 },
 {
   "NDB_NO": 43406,
   "Description": "Yeast extract spread",
   "Weight(g)": 6,
   "Measure": "1.0 tsp",
   "Protein(g)Per Measure": 1.43,
   "Carbohydrate, by difference(g)Per Measure": 1.23,
   "Sugars, total(g)Per Measure": "0.1"
 }
]
```

You can see that it is just a bunch of information about fruits and vegetables, including weight, measure, carbs, proteins, and sugars. We won't be using every field in this, but I'll show you in the next video how we customize the input. For now we're just going to be adding our grid and throwing that data inside of there with no customizations. We have everything we need imported, let’s look at what the top of the `App.js` file will now look like.

*`src/App.js`*
```js
import React, { Component } from 'react';
import { DropDownList } from '@progress/kendo-react-dropdowns';
import { NumericTextBox } from '@progress/kendo-react-inputs';
import { Button } from '@progress/kendo-react-buttons';
import { Grid, GridColumn as Column } from '@progress/kendo-react-grid';
import '@progress/kendo-theme-default/dist/all.css';
import nutrition from './nutrition.json';
import './App.css';
```

Now that we have all of the components imported to use in our application, I want to put our information for our grid inside of state. First, we’ll need to build a `constructor`. We'll go ahead and pass `props`, and also pass `props` to `super` in case we need it later. Next, we're going to declare `this.state` adding our nutrition information to `data`. Easy peasy! Inside our state, we need to also pass information to our `DropDownList` so it knows what to list. We could also make this dynamic, so that's why I'm putting it in state now in case later on we decide to make what goes inside of the `DropDownList` dynamic. Here is what we have now inside the `App` class:

*`src/App.js` cont’d*
```js
…
class App extends Component {
  constructor(props) {
    super(props)
    this.state = {
      data: nutrition,
      habitsOptions: [
        'Drink 1 Cup of Water',
        '1 Hour of Coding',
        '10 Pushups',
        'Eat Something Healthy',
        '1 Hour of Reading',
        '10 Minutes of Meditation'
      ]
    }
  };
…
```

Now that we have that data inside of state that we need, we'll go ahead and go inside of our `render` function and actually add the components inside the template. Let's make a nice little header first and inside there we will make a `div className='health-habits'`. This is where the list of the habits that the user enters will be added. For now we're going to leave that empty because we're just adding our components right now. We’ll make a `div` named `add-habits` and add the place that users can add their habits that they want to do. We add our `DropDownList` by adding its tag and inside there feed the data: `this.state.habitsOptions`. It is a self-closing tag for this component, so we can just put that on the same line. You can drop it down too if you like, whatever your preference is.

After that we then need to see how many times they want to iterate that healthy habit. That is where the `NumericTextbox` comes in. All you really need to do to add the component is open it up with the component name tag and then a self-closing. That’s the bare minimum of what you need to add and all we’ll add now. Next, we will add a `Button` below that to say, "Yes, please add that healthy habit." Then we can close out the `add-habits` section and start our new `div` for the `Grid`.

We can call this next div `className='nutrition-grid'`. The [`Grid` component](https://www.telerik.com/kendo-react-ui/components/grid/) is pretty straightforward. The first thing you do is open up your `Grid` component tag then attach your data by setting `data` to `this.state.data`. Remember inside of our state we declared that `data` equalled the nutrition JSON file.
Now, to put that data we will be using the columns from that file that we imported. The `GridColumn` that we brought in as `Column` will be calling on those columns of data. Inside of the `Grid` tags we're going to be adding the columns to our grid. We can decide which data columns from the JSON file goes into each of these grid columns. We open up the `Column` tag and give it a `field` that is exactly equal to what is listed in our JSON file. In our JSON file we have description listed as one of the headers, but we are going to use the `title` attribute to have it labeled as `food` in our app. Much more straightforward.
Then we add the other four columns to our grid. Once that’s set we can finally close out our grid and close out this div. Let’s take a look at what our template looks like now.

*`src/App.js` cont’d*
```js
…
render() {
    return (
      <div className="App">
        <h1> Healthy Things </h1>
        <div className='health-habits'>
          <h2> Healthy Habits </h2>
          <div className='habits-list'>
          </div>
          <div className='add-habits'>
            <DropDownList
              data={this.state.habitsOptions}
            />
            <NumericTextBox />
            <Button> Add Habit </Button>
          </div>
        </div>
        <div className='nutrition-grid'>
          <h2> 🥥 Healthy Fruits &amp; Veggies 🥦 </h2>
          <Grid
            data={this.state.data}>
            <Column field='Description' title='Food' />
            <Column field='Measure' title='Amount' />
            <Column field='Protein(g)Per Measure' title='Protein' />
            <Column field='Carbohydrate, by difference(g)Per Measure' title='Carbs' />
            <Column field='Sugars, total(g)Per Measure' title='Sugars' />
          </Grid>
        </div>
      </div>
    );
  }
…
```

We have npm still running so, we can take a look and see what we have. If we go back over to `localhost:3000`, we can see that we have a DropDownList with all of our lovely things inside of here. It looks good too because we have that default styling already in place. We have a `NumericTextBox` that, right now, you can pretty much put anything inside of, including negative numbers. We will be changing that up in the next post. Finally, we have a grid that keeps going on forever, but again, it's already styled, which is nice. We have our application running with a few components, styled well.

*add image*

[Here is the commit](https://github.com/tzmanics/kendoui-react-video-series/commit/cc0858c856a94175c8716790b5089b79c2a24652) that covers all the changes we made in this post. This is what the final `App.js` file will look like now:
*`src/App.js`*
```js
import React, { Component } from 'react';
import { DropDownList } from '@progress/kendo-react-dropdowns';
import { NumericTextBox } from '@progress/kendo-react-inputs';
import { Button } from '@progress/kendo-react-buttons';
import { Grid, GridColumn as Column } from '@progress/kendo-react-grid';
import '@progress/kendo-theme-default/dist/all.css';
import nutrition from './nutrition.json';
import './App.css';

class App extends Component {
  constructor(props) {
    super(props)
    this.state = {
      data: nutrition,
      habitsOptions: [
        'Drink 1 Cup of Water',
        '1 Hour of Coding',
        '10 Pushups',
        'Eat Something Healthy',
        '1 Hour of Reading',
        '10 Minutes of Meditation'
      ]
    }
  };

  render() {
    return (
      <div className="App">
        <h1> Healthy Things </h1>
        <div className='health-habits'>
          <h2> Healthy Habits </h2>
          <div className='habits-list'>
          </div>
          <div className='add-habits'>
            <DropDownList
              data={this.state.habitsOptions}
            />
            <NumericTextBox />
            <Button> Add Habit </Button>
          </div>
        </div>
        <div className='nutrition-grid'>
          <h2> 🥥 Healthy Fruits &amp; Veggies 🥦 </h2>
          <Grid
            data={this.state.data}>
            <Column field='Description' title='Food' />
            <Column field='Measure' title='Amount' />
            <Column field='Protein(g)Per Measure' title='Protein' />
            <Column field='Carbohydrate, by difference(g)Per Measure' title='Carbs' />
            <Column field='Sugars, total(g)Per Measure' title='Sugars' />
          </Grid>
        </div>
      </div>
    );
  }
}

export default App;
```

In the next post we'll be customizing it to make it work and act more like we prefer. We're going to wrap this one up here. If you have any questions, remember that you can reach out to us on Twitter [@KendoUI](https://twitter.com/kendoui) and me personally [@tzmanics](https://twitter.com/tzmanics). Stay tuned for the [next installment](). Thanks for coding with me. Hope to see you soon!