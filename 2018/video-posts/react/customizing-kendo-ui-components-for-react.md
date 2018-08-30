# Customizing Kendo UI Components for React

Hey everyone, it's me again, Tara Z. Manicsic, [tzmanics](https://twitter.com/tzmanics) on Twitter. I am here as a developer advocate for [Progress on our Kendo UI team](https://www.telerik.com/kendo-ui) talking about our library built from the ground up [for React](https://www.telerik.com/kendo-react-ui). This is a series where we're running through how to create a robust application using React and Kendo UI. This is the fourth installation in this series but all the posts and videos are listed below for you to follow along. We also have the repo with all the commits we've made so far [here](https://github.com/tzmanics/kendoui-react-video-series). If you have any questions, remember that you can find us at [@KendoUI](https://twitter.com/kendoui) on Twitter.

In the last post, we created the React application to hold all the components that we installed in [post two](). In the last installment, [post three](), we brought those components into our project. Now, in this video, we are going to be customizing the components to be more of what we need them to be. As a refresher, we are working with a [`NumericTextBox`](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/), [`DropdownLists`](https://www.telerik.com/kendo-react-ui/components/dropdowns/), [`Buttons`](https://www.telerik.com/kendo-react-ui/components/buttons/), and the famous [`Grid`](https://www.telerik.com/kendo-react-ui/components/grid/) component.

The first thing that we're going to look into is the [`NumericTextBox`](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/). We do have a [`DropdownList`](https://www.telerik.com/kendo-react-ui/components/inputs/dropdowns/) first, but we just added the data in the last post, and we were done. That's all we needed. We were like, "Listen dropdown list, that's all we need from you. Thanks." More importantly, our `NumericTextBox` is not looking exactly how we want it. Right out of the box it was basically inserting any numbers the user wanted, including negative numbers and decimals. We don't want people to eat negative amounts of fruit and veggies. I don't even know what that would be, and I don't want to know. As many times as I want to only halfway do some tasks, we don't want decimals in our values. This value will be turned into an amount of radio buttons, for the number of iterations of each habit, and we can't have .22 radio buttons. So, we need to prevent users from being able to enter negative and decimal values. In order to do that, we customize the `NumericTextBox` located in the template or render sections of the `App.js` file. The first property that we're going to add is `format`. To set the format for no decimals we set it to `0`. There are other formats to choose from. For instance, you can add `C` to format the input as currency. Today `0` is all we need. In the [documentation for the `NumericTextBox`](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/) there are all the different format types that you may need. There's also the whole [API](https://www.telerik.com/kendo-react-ui/components/inputs/api/NumericTextBox/) that you can go through and check all the ways you can customize the this input. Next, we're gonna set a `min` value to zero so that they cannot input any negative numbers. Just for the heck of it we'll also set a `max` value at `22`. Now we have the setup for our `NumericTextBox` to act as we need it to act. If we look back to our running app you can see, when you try to add a decimal, it gives me a red warning. This is another really nice UX detail that comes straight out of the box with the [Kendo UI default theme](https://www.telerik.com/kendo-react-ui/components/styling/theme-default/). You also aren't able to add any decimals. Can I add 56? No. It maxes out at 22. With the built-in keyboard navigation we can raise or lower the amount with the arrow keys but you still can't go all the way down past zero. So, we're good on that part.

*insert image*

So the next thing that we're going to do with our components is add some event listeners. If you recall, we created a section for there to be a list of the healthy habits that people are adding. In order to gather that information, we're going to add event listeners on both of the inputs and the button so that when they press a button, it adds it to the list. Before we get into those, let's add some information that we're going to use in `state`. We're going to adding data right under `data: nutrition`. First we're going to add `habitId` and set it to `0`. We're using this to set a key, since we need a key for every list item. Then we add `habit` for the name which we will leave blank. Followed by `habitIteration` for how many times they want to carry out the habit the enter, again initially setting it to `0`. After that we add our `habits` setting it to a blank array.

*`src/App.js`*
```js
this.state = {
   data: this.getNutrition(initialFilter),
   filter: initialFilter,
   habitId: 0,
   habitName: '',
   habitIteration: 0,
   habits: [],
...
```

With all this data in, we can start making our handler functions now. First, we will make `handleNameChange` passing in `event`. When this function is triggered we're going to `setState` to change our habit name. We'll set it to `event.target.value`. We're going to be doing the same thing to `handleIterationChange`.

*`src/App.js`*
```js
...
  handleNameChange = (event) => {
    this.setState({ habitName: event.target.value });
  }

  handleIterationChange = (event) => {
    this.setState({ habitIteration: event.target.value });
  }
...
```

Now that we have the functions, we have to add them to our inputs event listeners. Let's go back down to our inputs, and we'll add the `value` as `this.state.habitName`. Anytime there's a change in the inputs, it will tell state, "Hey, we need to update this to what we just put in here." We do the same with numeric text box setting `value` to `this.state.habitIteration`. Of course, in order to see that these actually worked, we're going to have to build out our list of habits these inputs are adding.

To get started, we are going to go down to our button and, to make this even lovelier, add the Kendo UI property of `primary` and set it to `true`. Next, we can add an `onClick` listener setting it to trigger a function we'll call `handleAddHabit`. We still need to make that.

*`src/App.js`*
```html
...
<div className='add-habits'>
            <DropDownList
              data={this.state.habitsOptions}
              value={this.state.habitName}
              onChange={this.handleNameChange}
            />
            <NumericTextBox
              format='0'
              min={0}
              max={22}
              value={this.state.habitIteration}
              onChange={this.handleIterationChange}
            />
            <Button primary={true} onClick={this.handleAddHabit}>
              Add Habit
            </Button>
          </div>
...
```

Now we'll go back up to the rest of where the functions live, and add this new function. We're setting more than we did in the last one because we need to add habits as an array. We will be concatenating each new addition to the rest as we add them. To do this we'll set the state of habits to concatenation of the array. Inside the `concat` function we add the information that we recieved from the other inputs (`habitId`,`habbitName`, and `habitIteration`).We can also set the `habitId` for the `key` value we'll need by adding 1 to the existing id.

*`src/App.js`*
```js
...
  handleAddHabit = (event) => {
    this.setState({
      habits: this.state.habits.concat([{
        key: this.state.habitId,
        name: this.state.habitName,
        iterations: this.state.habitIteration
      }]),
      habitId: this.state.habitId +1
    });
  }
...
```

We need to tell the render function how to render the list of habits. If we go back down to our template, we're going to add an unordered list of all of these habits. Inside that unordered list, we're going to map through that array of habits and display a list component for each of those. Then inside of the list component, we're going to take the value we have stored for the object's iteration and make an array with that amount of objects. Using that number we'll make that many inputs set to radio buttons. So, however many iterations they chose, they'll have a radio button to check for each time they carry out that habit.

To do this we first open up a `<ul>` tag and inside of there, we start our JavaScript code inside of curly brackets. To start we call on `this.state.habits.map` to iterate through our array of habits using `habit` as the iterator. For each of those habits we'll make a list item (`<li>`) and fill in the unique key of `habit.habitID`. Since we have multiple lines of of code for each list item and multiple things returned we'll wrap all this code in square brackets. This is the area for all of the radio button inputs too. To add these we'll make a new `div` for them and inside there use the spread operator (`...`) with `Array` to make an array the size of the value we have stored for `habit.iterations`. Then we, again, `map` over the newly made array and return an input for each iteration.

*`src/App.js`*
```html
...
          <div className='habits-list'>
            <ul key='all-habits'>
              {this.state.habits.map((habit) => [
                <li key={habit.habitId}>
                  <h3>{habit.name}</h3>
                  <div className='iterations-area'>
                    {[...Array(habit.iterations)].map((iteration, index) => {
                      return <input key={index} type='radio' />
                    })}
                  </div>
                </li>
              ])}
            </ul>
          </div>
...
```

Now we should see our list populated with the information that the user put into our inputs. Nice. So we have the habit is that they want to do, and a radio button for how many times they wanna do it. They can check them off as they go.

*add picture*

The next thing that we're going to do is work on making our grid not only look a little bit better, but also add some functionality by giving it the ability to filter. There is so much that you can customize and do to get the full potential out of the grid, but today, we will just be using the filtering. Since we have this never ending grid, we're going to set the height on it first by setting the `style` property to `{{maxHeight: '500px'}}`. We save that, and now we no longer have the crazy long grid.

Now we'll be adding the filtering for our grid. If you recall, in [the second installment]() we installed the data query module, so the first thing we need to do is import that. Then we'll set up an initial filter in the beginning. Right above `state`, we're gonna go ahead and set our `initialFilter` object with some information. Everything that we're setting now are actually properties that the user will have control over when they set their own filters in the web app.

*`src/App.js`*
```js
...
    const initialFilter = {
      logic: 'and',
      filters: [{
        field: 'Description',
        operator: 'contains',
        value: 'Apple'
      }]
    };
...
```

`Description` is that first field from the JSON nutrition data that we set as the first column describing the food. Next we'll set `operator` to `contains` which means we are looking to filter and show results where Description "contains" what we're looking for. To start us out, we're going to make the value of what we're looking for `Apple`. Again, this is just the initial filter that will be in place when we first render the grid.

Next, we're going to  head inside the state, and change the data that gets fed to the grid. We want to make sure that we're sending the grid the data that is filtered the correct way. To do that we'll make a function called `getNutrition` (we'll make that function next) and pass `initialFilter` which is the object we just made. Then we will also set `filter` to `initialFilter`.

We need to make the `handleFilterChange` and `getNutrition` function now. Let's go down to all the rest of our functions add them there after `handleAddHabit`. With `handleFilterChange` we want to pass the event then use `setState` to reassign `data` and `filter`. for `data` we want to pass `getNutrition` again and pass that the `event`'s filter. Then `filter` will also be set to `event.filter`. Working on `getNutrition` next we're going to pass it the `filter` which we initially set to `initialFilter` but will change when the user changes the filter settings. Then we're just going to return the nutrition data that has the filter applied to it by thanks to `filterBy` brought in when we imported `kendo-data-query`.

*`src/App.js`*
```js
...
  handleFilterChange = (event) => {
    this.setState({
      data: this.getNutrition(event.filter),
      filter: event.filter
    });
  }

  getNutrition = (filter) => filterBy(nutrition, filter);
...
```

Heading back down to out template we need to add some properties to the grid component to make it filterable. The three properties we'll add are `filterable`, `fiter`, and `filterChange`. First `filterable` will be set to `true` which is pretty self-explanatory. Next, the filter for the graph will be set to `this.state.filter` which we made to be updated at every change. Speaking of change, `filterChange` will be triggered each time the user changes one of the filters options. This will be set to the function we made earlier: `handleFilterChange`.

Phew that's a good amount for today! Remember that you have the project [repo](https://github.com/tzmanics/kendoui-react-video-series) along with all the other posts are listed down below. There are also more posts to come. Yes, there is more! We will talk about the different Kendo UI React wrappers for even more components that you can use inside of these React applications. We'll walk through other things, bonus material, in the last post too. So, I hope you check those out and I'll see you there. If you have any questions, you can reach out to us at [@KendoUI](https://twitter.com/kendoui) and me personally at [@tzmanics](https://twitter.com/tzmanics). Thank you very much for coding with me, and I hope to see you soon.