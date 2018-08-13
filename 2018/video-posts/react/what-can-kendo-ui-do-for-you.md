# What can Kendo UI for React do for you?

Hi, my name is Tara Z. Manicsic and I'm a Developer Advocate for Progress. Today, I'm here to talk to you about one of the new libraries from Kendo UI, [built specifically for React](https://www.telerik.com/kendo-react-ui). What is this Kendo UI I speak of?[Kendo UI](http://kendoui.com) is a user interface component library. These are components that range everywhere from things you would use everyday to robust interactive components like [Grids](https://www.telerik.com/kendo-react-ui/components/grid/) and [Data Visualizations](https://www.telerik.com/kendo-react-ui/components/charts/). For forms you could use our [inputs](https://www.telerik.com/kendo-react-ui/components/inputs/), [dropdown lists](https://www.telerik.com/kendo-react-ui/components/dropdowns/), [buttons](https://www.telerik.com/kendo-react-ui/components/buttons/), and more!
Why React? The Kendo UI team has been building component libraries for over 15 years, they have a lot of experience with user interface components. They've built them for [jQuery]( https://www.telerik.com/kendo-ui), [Angular](https://www.telerik.com/kendo-angular-ui/), [Vue]( https://www.telerik.com/kendo-vue-ui), and now they're out with a true library built specifically for React. Side note, when you have a license to get the React libraries, it also means that you have access to the jQuery and Vue and Angular libraries as well. Not that anybody would ever stray from React or have different projects where they use different libraries 😋. But, just in case, you have those libraries at your disposal.

Back to it, why React? Well they decided to build a library specifically for React, because React is cool 😎. Okay, but more importantly, a lot of developers use it, including myself and probably you. It is very popular. The Kendo UI team wanted to build a library helped making those React applications more efficient, faster, and easier. This is why we have a library that's specifically for React. This is to say no funny business behind the scenes with wrappers, although we do have [wrappers](https://www.telerik.com/kendo-react-ui/components/#react-wrappers) if that's what you prefer. This library, though, is built specifically for React. When you are building a React application and you use the Kendo UI components it still boils down to being an actual React application because these are true React components. What all does that mean for your React application? These React components are composable, you can precisely configure them to exactly whatever you need. This will give you more precision to make exactly what you want, customization. The components also support controlled and uncontrolled state. So, whatever mode you need, we got you.

What other components are there? I know that I gave you a list of a few of the components at the top of the video. But now I want to show you the full list of the current available components we have readily available for React.

[Animation](https://www.telerik.com/kendo-react-ui/components/animation/)
- [Expand](https://www.telerik.com/kendo-react-ui/components/animation/api/ExpandProps/)
- [Fade](https://www.telerik.com/kendo-react-ui/components/animation/api/FadeProps/)
- [Push](https://www.telerik.com/kendo-react-ui/components/animation/api/PushProps/)
- [Reveal](https://www.telerik.com/kendo-react-ui/components/animation/api/RevealProps/)
- [Slide](https://www.telerik.com/kendo-react-ui/components/animation/api/SlideProps/)
- [Zoom](https://www.telerik.com/kendo-react-ui/components/animation/api/ZoomProps/)

[Buttons](https://www.telerik.com/kendo-react-ui/components/buttons/)
- [Button](https://www.telerik.com/kendo-react-ui/components/buttons/button/)
- [ButtonGroup](https://www.telerik.com/kendo-react-ui/components/buttons/buttongroup/)

[Charts](https://www.telerik.com/kendo-react-ui/components/charts/)
- [Chart](https://www.telerik.com/kendo-react-ui/components/charts/chart/)
- [Sparkline](https://www.telerik.com/kendo-react-ui/components/charts/sparkline/)
- [Stock-Chart](https://www.telerik.com/kendo-react-ui/components/charts/stock-chart/)

[Conversational UI](https://www.telerik.com/kendo-react-ui/components/conversationalui/)

[DateInputs](https://www.telerik.com/kendo-react-ui/components/dateinputs/)
- [Calendar](https://www.telerik.com/kendo-react-ui/components/dateinputs/calendar/)
- [DateInput](https://www.telerik.com/kendo-react-ui/components/dateinputs/dateinput/)
- [DatePicker](https://www.telerik.com/kendo-react-ui/components/dateinputs/datepicker/)
- [TimePicker](https://www.telerik.com/kendo-react-ui/components/dateinputs/timepicker/)

[Dialog](https://www.telerik.com/kendo-react-ui/components/dialog/)

[DropDowns](https://www.telerik.com/kendo-react-ui/components/dropdowns/)
- [AutoComplete](https://www.telerik.com/kendo-react-ui/components/dropdowns/autocomplete/)
- [ComboBox](https://www.telerik.com/kendo-react-ui/components/dropdowns/combobox/)
- [DropDownList](https://www.telerik.com/kendo-react-ui/components/dropdowns/dropdownlist/)
- [MultiSelect](https://www.telerik.com/kendo-react-ui/components/dropdowns/multiselect/)

[Inputs](https://www.telerik.com/kendo-react-ui/components/inputs/)
- [NumericTextBox](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/)
- [Input](https://www.telerik.com/kendo-react-ui/components/inputs/input/)
- [Switch](https://www.telerik.com/kendo-react-ui/components/inputs/input/)

[Grid](https://www.telerik.com/kendo-react-ui/components/grid/)

[Layout](https://www.telerik.com/kendo-react-ui/components/layout/)
- [PanelBar](https://www.telerik.com/kendo-react-ui/components/layout/panelbar/)
- [TabStrip](https://www.telerik.com/kendo-react-ui/components/layout/tabstrip/)

[Popup](https://www.telerik.com/kendo-react-ui/components/layout/tabstrip/)

[Ripple](https://www.telerik.com/kendo-react-ui/components/ripple/)

It's a long list so feel free to go and check out the website [kendoui.com](http://kendoui.com) to get the real up-to-date component list of all the components we have available and a [roadmap](https://www.telerik.com/kendo-react-ui/roadmap/) to see what's coming. To use these components, all you need to do is install them using npm, import them into your project, and add them to your template.

`npm install @progress/kendo-react-ripple`
*src/App.js*
```js
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { Ripple } from '@progress/kendo-react-ripple';

class App extends React.Component {
  render() {
    return (
      <div className="example-wrapper">
        <Ripple>
          <p>Ripple on Buttons</p>
          <button>Primary Button</button>
        </Ripple>
      </div>
    );
  }
}
...
```

It's pretty easy, and that's basically the main syntactical pattern that you use every time you use our components.
One of my favorite parts about using the Kendo UI components is that they do a lot of the styling work for you. As a CS major, I can attest that styling is hard, CSS is hard. So one thing that you get with the Kendo UI components are theme libraries. That includes the [Kendo default theme](https://www.telerik.com/kendo-react-ui/components/styling/theme-default/), [Material](https://www.telerik.com/kendo-react-ui/components/styling/theme-material/) theme library, and [Bootstrap](https://www.telerik.com/kendo-react-ui/components/styling/theme-bootstrap/)theme library. With these libraries all you need to do, the very minimum thing that you can do, is install the theme with npm and then import it into your project. Let me get into like the next steps, the  really, really complicated steps. Just kidding. That's it, that's all you need to do if you want to easily incorporate style.

`npm install @progress/kendo-theme-default`

*src/App.js*
```js
import '@progress/kendo-theme-default/dist/all.css'
...
```

With that minimal amount of effort, the theme gives you lovely styled components where the style is consistent across your application, across all the components, even across projects. You don't really have to touch the CSS files, which I find very nice. But you also get different interactions and animations with these style libraries. All of the things that make your components really usable and really user friendly are included by including these style libraries. It’s pretty nice.

More, more, more, more, more. There is more that comes with these components that I want to talk to you about. Accessibility! Accessibility's important, you want as many people as possible to be using your application and to feel comfortable using your application. It can take time and it does take effort to add correct standard accessibility to your web application. When you use the Kendo UI components we give you a lot of [accessibility right out of the box](https://www.telerik.com/kendo-react-ui/components/animation/). This includes Section 508 compliance, W3C web content accessibility guidelines, WAI-ARIA and keyword navigation. Accessibility is important and now you don't have to put the dev hours into it, it comes with your components. Who doesn't want that? Who doesn't want easy accessibility to make your site better for everybody? You also get [internationalization](https://www.telerik.com/kendo-react-ui/components/globalization/i18n/). With any of the components that are using dates or numbers, like date input and your grids, numeric text box, etc., you get the internationalization wrapped up with the component when you install everything for the component. It's nice right? I think so.

There's one thing that I think everybody will always need at some point: help! Not that anybody has ever run into a problem they couldn't solve of their own. In those cases where you may hit some bumps or you may not understand something we offer different sources of help and support. This is includes an option for [24-7 human support](https://www.progress.com/services). You can also visit [community forums](https://www.telerik.com/forums/kendo-ui-react) where other people who are using the Kendo UI library as well as team members are in there to help you answer questions, have discussions, and talk about different strategies they used for the Kendo UI components that they've used in their products. There are even more resources like [interactive demos](https://www.telerik.com/support/demos) you can open up and mess things about. Then you can see what changes you want to try to implement inside of a live code demo. Along with that, we have [example projects](https://github.com/telerik/react-dashboard), [webinars](https://www.youtube.com/watch?v=GsQ_yATS7OY), [blog posts, and tutorials](http://www.telerik.com/blogs) that will give you more resources to help you. A little extra to help guide you beyond the documentation that we already have for each component.

I hope this post gave you a good understanding of what the [Kendo UI components](https://www.telerik.com/kendo-react-ui/components/) are, what they have to offer you, and everything that comes along with joining the Kendo UI community. We have a lot more coming up. I have some more posts in this series to walk you through exactly how to use the components by stepping through adding them, building a project with them, and moving on from there. This series also has an accompanying [video playlist], so check that out if you prefer posts in motion. In the mean time, if you have any questions at all, always feel free to reach out to us [@KendoUI](https://twitter.com/kendoui) on Twitter. You can always reach out to me on twitter too at [@tzmanics](https://twitter.com/tzmanics). Thank you for joining me on this Kendo UI for React journey, hope to code with you soon!