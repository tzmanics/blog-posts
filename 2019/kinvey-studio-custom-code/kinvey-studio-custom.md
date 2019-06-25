# Everything You Need with Kinvey Studio Custom Code

Kinvey Studio allows you to build web and mobile applications with ease. There are tons of features to let you easily build out layout, drag and drop elements and use pre-made layouts for a robust application. Sadly, it turns out our team isn't omnipotent so there may be some features you would like to add that we haven't already built components for. For cases like this, we've mad a custom component that lets you add the code you need to build out your application. Having the ability to add custom code will give you endless options.

Let me show you how to add your own code. To be totally honest, I was hard-pressed to find features I wanted to add that didn't already exist in our platform. Fear not, though, I thought of some good examples. First we'll make a really quick application that has login, a master list of all of items, a detail page for each item and a form to add more items. For this example, we're going to have a list of contractor tasks that need finished by an employee. 

Let's start building!

## Building a Base App with Kinvey Studio

### Login Page
When you create an app with Kinvey Studio a login page is pre-built for you, for both mobile and web. The app we're building today is for mobile and this is what that looks like:

![creating an app](create-login.gif)

As a default the login page will use your Users from your Kinvey backend. By default, the app will also have an option to register on the login page. When a user registers they are automatically added to the User list in your Kinvey backend. You can also easily add any other login options you want with Kinvey's [Mobile Identity Connect](https://devcenter.kinvey.com/rest/guides/mobile-identity-connect) service.

![logging in and registering](login-register.mov)

### Master List Page
Now that we can get users in, let's give them something to look at. We'll start by creating a list view of all the jobs a contractor has along with a line that states the progress of the job. To make a list view we just need to pick the layout we want and assign the data mappings from our collection.

![making a master list](jobs.gif)

As you can see, it's a pretty simple list but we're going to add more features to it next. The important thing right now is that we have all the projects in one place for easy browsing.

![a preview of the list](list-preview.mov)

### New Job Form
What's a list if the user can't add more? Kinvey Studio makes this really easy: simply click on the view's setting gear and choose 'Create Form'. Based on the data model of your collection it will instinctively choose the form inputs for each column entity. You can rearrange and customize the form more on its layout page.

![building a form](form.gif)

After you've got the form just how you want it, you can go back to the original view and add a button to click for a new job. We assign that buttons action to opening up the form we just created. Easy as pie ([here](https://knowyourphrase.com/easy-as-pie) is this idiom's origin story, if you were curious like me).

![form preiview](form-demo.mov)

### Details Page

We want the user to be able to see the detail of that job when they click it, so we'll need to create that detail page. For now, I'm going to use a pre-made layout and populated it by setting data mappings. This is the most simple, straightforward way to create the detail page. We just need to choose a layout then start populating it with components.

![making a details page](detail.gif)

We can even add a form that is also mapped to our collection to update information for the particular job we are viewing.

![demo of the detail page](detail-demo.mov)

### Adding Custom Detail Page
That was all quite easy, so easy, that I have extra time before my deadline. When is the last time you said that? With this extra time we can make the details page even more thorough and give our user more functionality by adding some features with custom code.

Resources

Outro
