# Building Better Forms With Kendo UI & Angular

We use forms almost everyday for login, sign up, purchases, etc., so the forms we make should be as painless as possible. [Kendo UI for Angular](http://www.telerik.com/kendo-angular-ui/) is a library of UI components that help you make great forms faster. We're going to create a few forms here to show some options for forms that won't make your users want to rip their hair out 😉. With each example we'll also look into why this may be a better option than what we typically see in the wild world of the web.

Besides what we'll cover when building these forms, there are three other great benefits of using the Kendo UI for Angular component library: built-in accessibility, default styling and native Angular components. The input and dropdown components in the Kendo UI library are compliant with [Section 508](https://www.section508.gov/) requirements, offer WAI-ARIA support, follow the  [WAI-ARIA best practices](https://www.w3.org/TR/wai-aria-practices/) for keyboard navigation and have been tested against popular screen readers. The input components also offer [Right-to-Left (RTL)](http://www.telerik.com/kendo-angular-ui/components/localization/rtl/) support (the ability to handle and respond to users who communicate through right-to-left languages such as Arabic, Hebrew, Chinese, and Japanese) as well as [Localization](http://www.telerik.com/kendo-angular-ui/components/localization/), which helps us translate components into different languages. Once we have the components added to our template we can include our default, Bootstrap or even a custom theme to take care of all our form styling. The [Kendo UI Theme Builder](http://www.telerik.com/kendo-angular-ui/components/styling/theme-builder/) makes it so we can try out the styles, see which one we like, then easily have it applied to all our components. Last, but definitely not least, these components aren't wrappers. The components are built from the ground up to be native Angular components, so we can take advantage of [AoT, Tree Shaking & Universal Rendering](http://www.telerik.com/kendo-angular-ui/components/framework/aot/) right out of the box!

If you're just getting started with with Kendo UI for Angular you can check out our [Getting Started documentation](http://www.telerik.com/kendo-angular-ui/getting-started/#installation) or this [Gif Guide to Getting Started](http://www.telerik.com/blogs/gif-guide-to-getting-started-with-kendo-ui).

Now, let's dig into these forms!

In this post we'll look into two main topics each with four points of focus:

__Inputs__
- Blind Password Entry
- Capitalization & Input Control
- Error Validation
- Options Types for Inputs


__Navigation__
- Form Field Focus
- Keyboard Navigation
- Progress Bar
- Form Field Title

## Inputs
Forms are really just a series of inputs but we have the opportunity to help users by creating different strategies to help them put their information into those inputs. For instance, how many times have you typed a password that was hidden and then thought, 🤔 "hmmm did I remember to put the '?' in the middle?" How about that rage that comes from filling out a whole form, just to have one field be wrong and then having to fill the whole form out again! 

![password rage](https://media.giphy.com/media/KFCqEnt8MWTxS/giphy.gif)

*Haven't we all felt this way at least once?*

There are little things too, like when you have to switch to the capital letter keyboard on your phone just to capitalize your first name in one field, then switch again to capitalize your last name in the next field.

### Blind Password Entry
The default for password input fields is to change each character a user types into an '*' to hide it from prying eyes and keep our password secret. I must admit thought, that I'm a big advocate for __not__ hiding passwords. Most of the time when I'm filling in a password I'm either at home or on my cell phone, so I'm not too worried about anyone else seeing what I'm typing. I'm much more concerned that I didn't type the password correctly so I tend to 1. questions myself 2. hit command + A to clear the whole field 3. start all over again (4. sometimes repeat steps 1-3 😡). So, maybe it's time to change how we create these password fields.


Let's see what if looks like by trying a password input that stays visible with an option to hide it and a hidden password field that gives us an option to see it. We'll use the word 'hide' in the first example and in the second we'll use the [Kendo UI Icon Font](http://www.telerik.com/kendo-angular-ui/components/styling/icons/) to set an eye icon for the user to reveal their password. 

*<password hide option and icon font example\>*
http://embed.plnkr.co/skLwMDUJhz4L2u8BiLNu/

### Capitalization & Input Control
The less thinking a user has to do while filling out the form the better. Small things like capitalizing the first letters of the 'first name' and 'surname' inputs can be a stress reducer as well, especially for mobile users. We can even make an input only take the characters we request. This is where Kendo UI's [Masked Text Box](http://www.telerik.com/kendo-angular-ui/components/inputs/maskedtextbox/) really shines. This input component let's us format the masked value when the user interacts with the component by pasting or typing in the input field. Here is an example of using a regular input to make sure the first letter is capitalized and using the Masked Text Box to format the user's input:

*<capitalization and Masked Text Box example\>*
http://embed.plnkr.co/2iHyuZHvzThRObOiDNS4/

### Error Validation
Validating each field as the user moves away from it helps them immediately realize the mistake and correct it. When using the masked text box, like we did above, we can now try the [built-in validation](http://www.telerik.com/kendo-angular-ui/components/inputs/maskedtextbox/#toc-validation). This allows us to check if the input is valid and gives us a property of `templateForm.valid` to set other properties, like we do in the example with the `disabled` property of the button. Now, if the input is not valid a user won't be able to submit their erroneous answers 🤘. 

*<masked text box validation example\>*
http://embed.plnkr.co/v3n32u9zGKMAdIetEPud/

### Options for Inputs
Technically, we _could_ have a plain ol' text box for every question on our form. *yawn* 😴 Instead of making our form monotonous and oh so boring, we can add sliders, multi-select dropdowns and switches. Kendo UI offers multiple [inputs](http://www.telerik.com/kendo-angular-ui/components/inputs/) types and [dropdown menus](http://www.telerik.com/kendo-angular-ui/components/dropdowns/0) so we can make our form easier and more intuitive to fill out. Check out a few of these options below for [date](http://www.telerik.com/kendo-angular-ui/components/dateinputs/), [yes/no](http://www.telerik.com/kendo-angular-ui/components/inputs/switch/) and [range](http://www.telerik.com/kendo-angular-ui/components/inputs/slider/) questions.

*<date input, switch and slider example\>*
http://embed.plnkr.co/FoUWd6m0uO2TT7Sf4aPW/

## Navigation
The process of filling a form out, especially long forms, can be quite tedious. One way to make it worse is by not directing a user through our forms. In this section, we'll look into how to help the user navigate by using focus, enabling them to use their keyboard to navigate through the form, updating the user on their progression and aiding them with static labels of the form's input fields.

### Form Field Focus
By directing the focus of our page to where the user is currently inputing data, we let them use that cognitive energy on the task at hand: inputting their information. We can set our very first form input to have autofocus so when the user opens the page with our form they can immediately start typing their responses. All of the Kendo UI inputs have a `focus` event emitter attached so we can even attach an interaction every time a user focuses on that input field.

*<autofocus input field & focus event emitter example\>*
http://embed.plnkr.co/BvEEf2CZ0avHcdnbsFPa/

### Keyboard Navigation
When users are typing their information sometimes it's easier for them to just leave their hands on their keys to navigate to the next input. This is where keyboard navigation in our forms would be much appreciated. All the Kendo UI input components come with [built-in keyboard navigation](http://www.telerik.com/kendo-angular-ui/components/dropdowns/dropdownlist/keyboard-navigation/). For instance, on the [switch input](http://www.telerik.com/kendo-angular-ui/components/inputs/switch/keyboard-navigation/) below you can hit the space bar to toggle your answer and in the [multi-select dropdown](http://www.telerik.com/kendo-angular-ui/components/dropdowns/multiselect/keyboard-navigation/) we can press the down arrow to go through the list and hit enter on each new selection. 

*<switch & multi-select dropdown example\>*
http://embed.plnkr.co/Nxat94IUk06GPEMHNYMY/

### Progress Bar
Is this form still going? Will it ever end? Where am I??

![lost bill nye](https://media.giphy.com/media/3o7bu93TZgndzlVvri/giphy.gif)

Okay, maybe it's not _that_ dramatic but there is something very relieving about being told we are 75% finished with a form. We can also guide our users by letting them know which question they are on and how many more there are to go. Below is an example of a type of counter that takes into account how many total inputs there are and how many the user has finished. 

*<interactive number update example\>*
http://embed.plnkr.co/a6zlj1gbGRUwVhxlyoVQ/

### Form Field Title
As creators of our forms, we will always know the form better than our users. So, we should not assume that when the user tabs to the next input field, we can take away the indicator of what they're supposed type into that input field. This is why we should keep a label our form inputs labeled even while a user is typing their responses. Here we can try a few different label placements to see which one fits the style of our site or the amount of space we have for our form.

*<form labels example\>*
http://embed.plnkr.co/BRosj7bY1l1obWIH90xo/

## Your turn 😁

Now that you have snippets of code and all these ideas, check out the [Kendo UI for Angular components](http://www.telerik.com/kendo-angular-ui/components/) to try it for yourself. Let me know if you have or create even better ways for us to make frustration-free forms. Can't wait to see what you create! Happy coding 🤙 

![have a go](https://media.tenor.com/images/dcb54f3811ac0d08dde5ad261c23326a/tenor.gif)

__Resources List__
- [Kendo UI for Angular](http://www.telerik.com/kendo-angular-ui/)
- [Section 508](https://www.section508.gov/)
- [WAI-ARIA best practices](https://www.w3.org/TR/wai-aria-practices/)
- [Right-to-Left (RTL)](http://www.telerik.com/kendo-angular-ui/components/localization/rtl/)
- [Localization](http://www.telerik.com/kendo-angular-ui/components/localization/)
- [Kendo UI Theme Builder](http://www.telerik.com/kendo-angular-ui/components/styling/theme-builder/)
- [AoT, Tree Shaking & Universal Rendering](http://www.telerik.com/kendo-angular-ui/components/framework/aot/)
- [Getting Started Documentation](http://www.telerik.com/kendo-angular-ui/getting-started/#installation)
- [Gif Guide to Getting Started](http://www.telerik.com/blogs/gif-guide-to-getting-started-with-kendo-ui)
- [Kendo UI Icon Font](http://www.telerik.com/kendo-angular-ui/components/styling/icons/) 
- [Masked Text Box](http://www.telerik.com/kendo-angular-ui/components/inputs/maskedtextbox/)
- [Kendo UI Input Components](http://www.telerik.com/kendo-angular-ui/components/inputs/)
- [Kendo UI Dropdown Components](http://www.telerik.com/kendo-angular-ui/components/dropdowns/0)

