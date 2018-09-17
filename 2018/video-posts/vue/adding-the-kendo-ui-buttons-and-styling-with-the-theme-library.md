# Adding the Kendo UI Buttons and Styling with the Theme Library

Hi, my name is Tara Manicsic, [@tzmanics](https://twitter.com/tzmanics) on Twitter and [GitHub](https://github.com/tzmanics). I am here today on post three of our Kendo UI ❤s Vue [series](link to all blog posts). This is the corresponding blog posts to the video series you can find on [out Youtube channel](https://www.youtube.com/watch?v=YLPLafiKd3E). In this post, we are continuing our project that we created in the [last installment]() using the Vue CLI. Today we will be building out a way for users to listen to an audio file by clicking a button. Then they can vote on a certain pronunciation by clicking a radio button and submit that vote by clicking another button. We're basically taking the components that we installed in the last post, and putting them into the project that we created.

Let's go ahead and jump in. Right now, we are in the main project directory that was made when we created our project using `vue init` using the Vue CLI. We can go ahead and go inside of the `src` directory, because that's where we're doing our work today. The first file that we want to look at is `main.js` file. This is where we will be importing `Button` and the button installer: `ButtonsInstaller`. These are from the module that we installed from at progress: `@progress/kendo-buttons-vue-wrapper`. Using those buttons also means that we'll want to import the theme that we brought in. Since we're using Kendo UI, we also want to import the Kendo UI library. 

*`src/main.js`*
```js
...
import {
  Button,
  ButtonsInstaller
} from '@progress/kendo-buttons-vue-wrapper'
import '@progress/kendo-theme-default/dist/all.css'
import '@progress/kendo-ui'
...
```

We have everything we need. We'll take advantage of `Vue.use` to bring in the buttons installer. And last but not least, we add it to our components list down here in our new Vuei object, and save that.

*`src/main/js`*
```js
...
Vue.use(ButtonsInstaller)

/* eslint-disable no-new */
new Vue({
  el: '#app',
  template: '<App/>',
  components: {
    App,
    Button
  }
})
```

Let's head over to the main vue component, which is `app.vue`, and per usual: to create, we must destroy. So, let's get rid of basically everything here, up to that `Hello` component. We're actually just going to rename it to what we want our new component to be, `TermList`. Then we'll change the file path, the file name in the directory and, finally, change it down in the `components` object in the export section too. It may have been just as easy to create a new file and get rid of this one, but what fun is that. Let's go ahead and delete all of this styling we have down in the style section as well so we can do our own custom styling later.

While we're in here, let's go ahead and make a new header and a subheader size h4. We're pretty much done until we come back to style this one. So let's save that, and move on to that terms list component that we just renamed.

*`src/main.js`*
```jsx
<template>
  <div id="app">
    <h1> H D Y P T </h1>
    <h4> a site that asks, 'How do you pronounce that?' </h4>
    <term-list></term-list>
  </div>
</template>

<script>
import TermList from './components/TermList'
export default {
  name: 'app',
  components: {
    TermList
  }
}
</script>

<style>
</style>
```

Now what once was `src/components/Hello.vue` we've renamed to `src/components/TermList.vue`. We will now open it up and prepare to destroy everything inside there.

*`src/components/TermList.vue`*
```jsx
<template>
</template>

<script>
export default {
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
```

Now our template is empty. We'll start in the template by creating a div for the term list and one for the encompassing box we'll put each term in. Let's call it `term-box`. Next we'll make a div for each term, one for the term definition and finally one for term pronunciations. Inside that final div (`<div class='term-pronunciations'>`) is where we're going to be doing our button work.

The first input we want is a place where users can click a radio button to select which pronunciation they want vote on. We're going to set the [`v-model`](https://vuejs.org/v2/guide/forms.html) to `selected` so we can keep track. We're going to name the input `vote` and we're going to set the value to equal zero aka not checked. That's all we need for the radio button.

Next, we want to add a button the user can click to hear the the first pronunciation. For this functionality  we get to add our Kendo [`Button`](https://www.telerik.com/kendo-vue-ui/components/buttons/button/) component. The button is added just by adding `<kendo-button` and setting some properties before closig out the tag with a `>`. I chose the Kendo UI button because it allows us to easily set an image for the button by setting the `icon` property. Having an icon for the button lets the user know that this button will play a sound without the language barrier of having to use words. Since we installed the default Kendo UI theme we can take advantage of the [`icon font`](https://www.telerik.com/kendo-vue-ui/components/styling/icons/) which has a ton of different useful icons to choose from. We'll use the icon that looks like a speaker here by setting `icon='volume-up`. Finally, we will listen for them to click the button with `@click` and set that to play the sounds file for that pronunciation. Now we can copy everything we just did, from the radio buton to the Kendo UI button. The only thing we need to change for the next iteration is the link for `playSound()` and the button text. The `name` for the radio button stays the same so they can only select one of the radio buttons.

Finally, we'll add another div called `term-voting`. In here, we're going to add another Kendo button, but we are going to make it stick out by adding `class='k-primary'`. This styles the button to use the accent color. We're going to again listen to the click event, but this time, we'll trigger a method called `onVote`. We don't need to pass anything to this function, we're just saying, "Hey, they voted." We'll have this button text read `Vote`, and close out our last and final Kendo UI button.

This is what out whole template looks like now:

*`src/components/TermList.vue`*
```jsx
<template>
  <div class='term-list'>
    <div class='term-box'>
      <div class='term'>
        <h2> GIF </h2>
        <p class='term-definition'>
          a lossless format for image files that supports both animated and
          static images.
        </p>
        <div class='term-pronunciations'>
          <input type='radio' v-model='selected' name='vote' :value='0' />
          <kendo-button
            icon='volume-up'
            @click='playSound("http://bit.ly/2HHjJio")'
          > gif
          </kendo-button>
          <input type='radio' v-model='selected' name='vote' :value='1' />
          <kendo-button
            icon='volume-up'
            @click='playSound("http://bit.ly/2plmOO2")'
          > jif
          </kendo-button>
        </div>
        <div class='term-voting'>
          <kendo-button class='k-primary' @click='onVote'>
            VOTE
          </kendo-button>
        </div>
      </div>
    </div>
  </div>
</template>
...
```

Now that the template is done, it's time to add the information that we're going to be passing to data. Head down to the `<script>` tag and the first thing that we're going to pass through is selected, which we talked about was that vue model, and we had originally set it to zero and it's own way to keep track of which radio button has been `selected` and set it to `0`. We also need to keep track of the votes for each pronunciation, so we add a variable for each. Now that we have those in place, we can add our methods.

The first method we'll add is the `playSound` method that we had passed our sound link to. Inside there, we'll be safe and say if we're passing something in for `sound`, let `audio` equal `new Audio` and pass it the sound link we passed through. Once audio has that, we'll call on `audio`'s `play` method passing it the sound to play. We haz play sound! Time for `onVote`. We're not passing the function anything and immediately checking `this.selected`. If you recall, we had `selected` set to `0` for the first pronunciation option. In this case `0` would be equal to false and out function would want to increment the votes for `pronunciation1Votes`. When the user chooses option 2 `selected`'s value is `1` which would equal `true`. Therefore we have `if (this.selected)` is true, increment `this.pronunciation2Votes` otherwise increment `this.pronuciation2Votes`. Just so we can keep track and know that this is all going how we expected it to, we'll `console.log out this information.

Here is what our `methods` section look like now:

*`src/components/TermList.vue`*
'''js
...
methods: {
  playSound (sound) {
    if (sound) {
      let audio = new Audio(sound)
      audio.play(sound)
    }
  },
  onVote () {
    if (this.selected) this.pronunciation2Votes++
    else this.pronunciation1Votes++
    console.log(
      '1: %s, 2: %s', this.pronunciation1Votes, this.pronunciation2Votes
    )
  }
}
...
```

Woo. Okay. So it looks like we have everything that we wanted.

*insert image*

Now let's take a look at what we're getting in our console. If we hit vote now, we'll have one vote for pronunctiation one, then two votes for one, and one vote for pronuncation two.

*insert images*

Everything is working swimmingly. That is where we are going to end things on this post with our voting functionality set, our buttons where they're supposed to be, doing the things they're supposed to do. In the [next post]() we will cover adding the [Kendo UI Chart]() so that we can visualize this information we're getting from the voting. Hopefully we will see you in the next installment. Remember, if you have any questions whatsoever, please feel free to reach out to us on Twitter [@KendoUI](https://twitter.com/kendoui). You can also reach out to me, [@tzmanics](https://twitter.com/tzmanics), on Twitter. Thank you for coding with me todayr!
