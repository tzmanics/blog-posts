# React 16.4.0 & 16.4.1 Releases

The Facebook team has definitely been busy these past few months with the minor release, 16.4.0, it’s follow-up patch, 16.4.1. We’ll walk through a few things that came from this release including Pointer Events, the next steps towards asynchronous programming, and more. You can keep up-to-date with all React’s releases on their GitHub repo’s [releases page](https://github.com/facebook/react/releases).

## Pointer Events

In order to keep track of users’ interaction with the page we have to now go beyond just mouse input. This is because people are browsing apps on more devices with more inputs whether it’s using a stylus on a tablet or their thumbs on a cell phone. To track all these inputs we now have have Pointer Events which inherit mouse events and add the ability to listen to touch and stylus interactions as well. Here is the list of new events available in React 16.4.0:

- `onPointerDown`
- `onPointerMove`
- `onPointerUp`
- `onPointerCancel`
- `onGotPointerCapture`
- `onLostPointerCapture`
- `onPointerEnter`
- `onPointerLeave`
- `onPointerOver`
- `onPointerOut`

*Note: the events only work where browsers support Pointer Events specification.*

## Next Steps for `getDerviedStateFromProps`

In the recent releases the React team has been making strides toward more asynchronous coding in React. Unfortunately, they also noticed developers making coding decisions that lead to unsafe practices and anti-patterns. The first step was to deem `componentWillMount`, `componentWIllUpdate`, and `componentWillReceiveProps` as `UNSAFE_` by literally adding that to their names. Then they brought in one of the first replacements: `getDerivedStateFrom Props`. In the latest minor release the team included a bugfix for `getDerivedStateFromProps` that made some existing bugs in React components apparent and more consistent, especially if your app was using an anti-pattern. The team is still in the process of making improvements so stay tuned.

## Fixes and Experimentals
The latest two releases also provided many fixes. You can see all of them listed in our blog post covering theses last two releases in detail: [New Features and Fixes We Got with the Latest React Releases](https://www.telerik.com/blogs/new-features-and-fixes-we-got-with-the-latest-react-releases). There was also a new experimental component that was released in 16.4.0, `Profiler`. With this new component from Brian Vaughn you can collect new time metrics. Right now most of the new functionality is behind a flag, `enableProfileModeMetrics` so without enabling it you component will render its children normally. When enabled this component will collect timing information and pass it to the `onRender` function.

The React team is keeping a steady stream of releases going so check-in at their [release page](https://github.com/facebook/react/releases) or check-in here for a comprehensive overview. Until the next release, happy coding!
