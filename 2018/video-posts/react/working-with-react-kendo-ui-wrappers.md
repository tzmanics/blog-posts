# Customizing Kendo UI Components for React

Hi, everyone, Tara Z. Mancisic here. I am a developer advocate for [Progress](https://www.progress.com/https://www.progress.com/), and I am here in this video to guide you through the awesome new library built from the ground up for [React from Kendo UI](https://www.telerik.com/kendo-react-ui). In this series so far, we have created a pretty robust React application. If you're like "Tara, I don't have an application made already," well, I'm sorry to break it to you, but you are on installment five out of six in this series. The whole list of blog posts can be found [here]() as well as the corresponding video series [here](https://www.youtube.com/watch?v=3goM9S5vFDo&list=PLLGlTD7u3kMo1TKLmFShXMhP-fIculjOu). There is also a [repository](https://github.com/tzmanics/kendoui-react-video-series) that we made in GitHub to walk you through all the code and show you all the changes we made through different commits so that you can catch up. Feel free to go there and then come back.

If you have been following along and you're like "Tara, what more could we possibly code in this amazing application?" Well, I want to show you that we also have [React wrappers](https://www.telerik.com/kendo-react-ui/components/#react-wrappers) at our disposal. The Kendo UI team released these before releasing the library that they built from the ground up for React. Today, we are going to look at the [Chart component](https://www.telerik.com/kendo-react-ui/components/charts/) for some data visualizations. We're going to allow the user to put some numbers into three sections to create a pie graph to visualize the difference between them. In the grid that we made we had proteins, sugars, and carbs for the fruits and vegetables. We'll allow users to input these numbers and see how they look in a visualization using the pie chart component. To use the charts component, we first install it, then import it into the project, add it to our template, bind the data from the user input, and finally check out our awesome graph.

First things first we need to install our component with npm, plus the Kendo UI library.

`npm install @progress/kendo-charts-react-wrapper @progress/kendo-ui `

If you notice in the other posts, we have a different syntax for installing these components. Instead of `@progress/kendo-react-<compnent-name>`, it's `@progress/kendo-<component-name>-react-wrapper`. 

*UPDATE: since creating this post the `Chart` component has been add to the [native React components](https://www.telerik.com/kendo-react-ui/components/charts/). Yay! That means that you only have to use the wrapper for `Chart` components if that is your preference.*

Next, we want to bring the component into our template. Go all the way down to where our `render` function, underneath our grid, we'll add it there. We'll give it a comfy little `div` to live in and, like the other components, we open it up with the angle bracket and component name: `<Chart`. We're going to send it `seriesDefaults = {this.state.seriesDefaults}`, and I'll show you what we're going to put in there later in this post. All the information we're sending to our chart will be listed in `this.state` inside out script, we'll look at that once we have our chart set up. The next attribur: `series`, is the information; the data that you're passing to your chart. We're going to set it to `this.state.series` and we're holding this in `state` because we're actually going to get the information from our user's form inputs. This is what the template code for your chart will look like so far:

```html
<Chart
  seriesDefaults={this.state.seriesDefaults}
  series={this.state.series}
/>
```

If we take a look at the [documentation for our chart](https://www.telerik.com/kendo-react-ui/components/charts/), there is also a lot of information on different things that we can change and add to our chart to customize it even more. Today we're going to keep it pretty simple.

We have the chart in, now I would also like to add the inputs where we want to get the user information to fill up that data visualization. First, we'll add a `div className=food-graph-inputs`. Then we will add a label to say that this section is for the 'Protein Amount'. Inside there we'll have an input that is `type=text` and listen for `onChange`, like we did with our other inputs. Next, we're going to have `onChange` run a function we'll add up top in our script called `handleProteinChange`. Finally, we close out the `input`. We want these for proteins, carbs, and sugars, so we’ll just need to repeat all these steps for each of those inputs.

```html
<div className='food-graph-input'>
  <p>Protein Amount:
  <input
    type='text'
    onChange={this.handleProteinChange} /></p>
  <p>Carb Amount:
  <input
    type='text'
    onChange={this.handleCarbChange} /></p>
  <p>Sugar Amount:
  <input
    type='text'
    onChange={this.handleSugarChange} /></p>
</div>
```

We now have inputs where the user can add this information. Let's go back up top to `state` to add some information we need to store. First, we're going to set `series` so it has something to put in the chart before a user adds anything. We'll just set it to a simple `1,1,1`. Then we set the `seriesDefaults` that we talked about earlier. Again, there's a lot of things that you can set here, but today we're just going to keep it simple but you can refer the [Chart documentation](https://www.telerik.com/kendo-react-ui/components/charts/) to see all the ways you can customize it. Talking about all of this healthy stuff puts me in the mood for pie. A pie chart, that is, obviously! We want to have a variable to hold our protein amount, carb amount, and sugar amount in the graph. So, we'll add `graphProtein`, `graphCarb`, `graphSugar`, and assign all of them to `1`. That's it, that's all that we need to save in state.

```js
this.state = {
  ...
  series: [{data: [1, 1, 1]}],
  seriesDefaults: {type: 'pie'},
  graphProtein: 1,
  graphCarb: 1,
  graphSugar: 1
};
```

Let's go ahead and create those functions that we need to go off whenever there is a change in the inputs we just made. That includes the `handleProteinChange`, `handleCarbChange`, and `handleSugarChange` functions. They will look a lot like our `handleNameChange` function. We're setting `state` like we did in our other handle functions. For this one, since we want the graph to change as the user puts this information in, we're also going to set off an event to update the graph: `handleGraphChange`. We’ll replicate it all of this for the other functions. Let's go on to our `handleGraphChange` function that we want to make here. This isn't going to use anything calling the event, so we won't pass that to the function. We _are_ going to set state again, setting it to `series` which we had previously set to `1,1,1`. We're assigning the `data` inside that to an array containing all of those inputs that we made from the user input.

```js
 handleProteinChange = (event) => {
  this.setState({ graphProtein: event.target.value });
  this.handleGraphChange();
}

handleCarbChange = (event) => {
  this.setState({ graphCarb: event.target.value });
  this.handleGraphChange();
}

handleSugarChange = (event) => {
  this.setState({ graphSugar: event.target.value });
  this.handleGraphChange();
}

handleGraphChange = () => {
  this.setState({
    series: [{
      data: [
        this.state.graphProtein, this.state.graphCarb, this.state.graphSugar
      ]
    }]
  });
}
```

Now, we have the functions that we need to update the graph when the inputs have information. As you see, there's a lot of repetition going on. So this is definitely something that I would refactor in the future. Or, if you have any ideas of how to refactor it, go for it and let me know how you decide to clean that up.

We have everything that we need to make our graph work. Let's take a look at this graph.

*insert image of graph*

We now have a reactive graph that is styled all on its own. Nothing we had to do besides insert that default theme and we are golden. That is how you use the React wrappers library. Pretty similar to the true React components, but now you have even more components.

That's a wrap for this post (get it?). Before you get too sad, there is one more video & blog post left in the series where we cover very exciting extras. For instance, did you know you have been coding a [Progressive Web App](https://www.telerik.com/blogs/gif-guide-creating-a-progressive-web-app-react-kendo-ui) this whole time? Shocking, I know. We'll delve into that and explain it more in detail in the next post, along with covering the rest of the components that are at your disposal. There are so many other ones that we were not able to touch on in this video series, but we'll look into those next! We'll look at even more resources that you have available to you, beyond this amazing series, to help you make amazing things with our component libraries. Remember, you can always reach out to us on Twitter, [@KendoUI](https://twitter.com/kendoui), and me personally, [@tzmanics](https://twitter.com/tzmanics), if you have any questions at all or just want to chat. Thanks for coding with me!