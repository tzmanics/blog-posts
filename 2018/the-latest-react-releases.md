# The Latest React Releases (16.4.0 & 16.4.1)

With the newest minor release of React, 16.4, plus a subsequent patch, 16.4.1, we’ve received lots of fixes, support for Pointer Events, some help with `getDerivedStateFromProps()`, and a few experimental features. It has been less than 2 months since we’ve had the 16.4 sweet release that gave us great updates like the official support of the context API. Instead of living in the past let’s look at the new shiny things we get with the latest releases.

* Just a reminder, you can always keep in-the-know with the latest releases [here](https://github.com/facebook/react/releases) in the project repo. *

##  Pointer Events

Probably the shiniest of the shiny for the 16.4.0 release was the support for Pointer Events. This was a feature that people requested often to be able to be aware of the following events:
`onPointerDown`
`onPointerMove`
`onPointerUp`
`onPointerCancel`
`onGotPointerCapture`
`onLostPointerCapture`
`onPointerEnter`
`onPointerLeave`
`onPointerOver`
`onPointerOut`

For a long time we’ve had access to mouse events to help us understand how a user was interacting with the application. Now users are interacting with more than a mouse, instead using touch or a stylus, for example. Pointer Events inherit mouse events so we can still take in that information while expanding to different forms of input interaction.

There’s a great example for you to play with [here](https://codesandbox.io/s/q83r7nrwv6) at CodeSandbox. In the example there is a circle on the page that listens to the `setPointerCapture` and other Point Events to move the circle corresponding to the interaction of a pointer. I was able to move it with the mouse/trackpad and with touch in Chrome but when I tried to move it with Pixelbook Pen I received an `InvalidPointerId` error.  Out of curiosity I tried the Surface Pro and it’s pen which returned the same `InvalidPointerId` error in Chrome but worked just fine in Firefox and Edge.

Here’s a little example of the code from the CodeSandbox example where it utilizes Pointer Events:

```html
     <div style={boxStyle}>
        <div
          style={circleStyle}
          onPointerDown={this.onDown}
          onPointerMove={this.onMove}
          onPointerUp={this.onUp}
          onPointerCancel={this.onUp}
          onGotPointerCapture={this.onGotCapture}
          onLostPointerCapture={this.onLostCapture}
        />
      </div>
```

Before you get too excited and use this everywhere, the events only work where browsers support Pointer Events specification. According to [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Pointer_events), right now that’s pretty much on all browsers on desktop and mobile except Safari. As I stated above there may also be a problem with using styluses on Chrome as well.

## Issues with `getDerivedStateFromProps`

In working to implement async rendering the React team noticed some cases where the legacy component lifecycle could was encouraging some unsafe coding practices. This was noticed with `componentWillMount`, `componentWIllUpdate`, and `componentWillReceiveProps`. After deeming these unsafe and literally adding `UNSAFE_` to the old lifecycle names, they brought out a replacement starting with `getDerivedStateFromProps`.

```js
class Example extends React.Component {
  static getDerivedStateFromProps(props, state) {
    // ...
  }
}
```
This new lifecycle should handle everything that we once used `componentWillReceiveProps` for when used with `componentDidUpdate. `getDerivedStateFromProps` is invoked after a component is instantiated and also when it receives new props. Straight from an [article](https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html) by [Brian Vaughn](https://github.com/bvaughn), 

>”It can return an object to update `state`, or `null` to indicate that the new `props` do not require any `state` updates.”

The release of 16.4 included a bugfix for `getDerivedStateFromProps` that made some existing bugs in React components apparent and more consistent, especially if it your app was using an anti-pattern. The React team has noticed developers getting confused about how to use `getDerivedState` (and `componentWillRecieveProps`) and are hoping to push changes and point out cases where they have been misused. They are persistent in reminding developers that the only purpose `getDerivedStateFromProps` should be used for is to update a component’s internal state when there are __changes in props__. They also want to remind everyone that it should be used sparingly. Brian Vaughn wrote a [post](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html) on some anti-patterns when using `getDerivedStateFromProps` and recommended alternate solutions. Before you write out that super long name, I highly recommend reading that article.

## List of Fixes from 16.4.0 & 16.4.1
There were lots of fixes in these last two recent minor and patch release. Here is a list of the combined list for your viewing pleasure:

### React DOM
Fix a crash when the input `type` changes from some other types to text.
Fix a crash in IE11 when restoring focus to an SVG element.
Fix a range input not updating in some cases.
Fix input validation triggering unnecessarily in Firefox.
Fix an incorrect `event.target` value for the onChange event in IE9.
Fix a false positive error when returning an empty `<React.Fragment />` from a component.
Fix a false positive warning when using `react-lifecycles-compat` in `<StrictMode>`.
Fix a bug that prevented context propagation in some cases.
Fix re-rendering of components using `forwardRef()` on a deeper `setState()`.
Fix some attributes incorrectly getting removed from custom element nodes.
Fix context providers to not bail out on children if there's a legacy context provider above.

### React DOM Server
Fix an incorrect value being provided by new context API.

### React Test Render
Fix `getDerivedStateFromProps()` in the shallow renderer to not discard the pending state. 
Fix the `getDerivedStateFromProps()` support to match the new React DOM behavior.
Fix a `testInstance.parent` crash when the parent is a fragment or another special node.

### React ART
Fix reading context provided from the tree managed by React DOM.

To learn more about each of these fixes you can check out their authors and github issues all listed on the [React Releases github page](https://github.com/facebook/react/releases).

## But Wait, There’s More

Along with that long list of fixes you also received some other goodies with the past two releases.

React
You can now assign `propTypes` to components returned by `React.ForwardRef`.

React Test Renderer
Allow multiple root children in test renderer traversal API.
`forwardRef()` components are now discoverable by the test renderer traversal methods.
Shallow renderer now ignores `setState()` updaters that return `null` or `undefined`.

React DOM
Change internal event names. This can break third-party packages that rely on React internals in unsupported ways.
Warn when the `forwardRef()` render function has `propTypes` or `defaultProps`.
Improve how `forwardRef()` and context consumers are displayed in the component stack.
Add the ability to specify `propTypes` on a context provider component.

I hope that something on your wishlist got checked off here. You can always keep asking for the changes you want on React’s [repo](https://github.com/facebook/react/issues). Fingers crossed! Better yet, feel free to uncross those fingers and use them to make the fixes yourself by following their [contribution guide](https://github.com/facebook/react/blob/master/CONTRIBUTING.md).

## Time for Experiments

There was also a new experimental `Profiler` component for all you React mad scientists out there. This new component allows you to collect new time metrics. When using this component you can have React collect timing information and pass it to the `onRender` function. For now, most of the functionality for this new component is hidden behind the `enableProfileModeMetrics` flag. When the flag is disabled the component will render its children normally. Here’s a little snippet of code from [Brian Vaughn’s PR](https://github.com/facebook/react/pull/12745):

```js
const Profiler = React.unstable_Profiler;

render(
  {/* Components not measured... */}
  <Profiler id="some identifier" onRender={loggingFunction}>
    {/* Components to be measured... */}
  </Profiler>
  {/* Components not measured... */}
);
```

## Keep Up

You can check out all the details, commits and more for all the latest React release information on their [repo](https://github.com/facebook/react/releases). It’s easy to tell the React team has been busy and are showing no signs of slowing. This is one of the reasons the [Kendo UI](https://www.telerik.com/kendo-react-ui) team has rolling releases to make sure we keep up-to-date to help you build your React apps faster. Hope you’re getting all the React features and fixes you were hoping for. Until the next release, Happy Coding!
