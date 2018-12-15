# Kinvey for Node Developers

Being a Node developer can span across many different types of programming these days because Node can be used for so much, from front-end to back-end, machine learning to IoT. I started my career as a Node engineer mostly working on the back-end and have watched Node grow to surpass many programming languages in usage and popularity. The Node ecosystem and community have also thrived and evolved each year. When I joined the Kinvey team, I was excited by all the ways the platform aligned itself with Node and lent itself to the ways I was already programming with Node. I wanted to point a few out to you today, so you could be excited too 😉.

## Built _by_ Node Developers
Kinvey is actually built using Node so we've got a lot of Node devs creating what you're using. Being Node developers helps us realize what is important for fellow Node developers. For instance, we recently made it so that you can use any LTS version of Node. You just chose the version you like and we install the latest patch of that major version. From here on out we will be aligned with Node's release schedule to stay up-to-date and also avoid any complications with versions of Node that are no longer under maintenance.

![node release schedule](https://raw.githubusercontent.com/nodejs/Release/master/schedule.png)

We also know the value of the Node ecosystem. We have members of our team who have contributed to Node core and are active in the Node community. We also utilize the npm ecosystem with our Flex Services to make it easy for you to incorporate them into your projects. [Kinvey FlexServices](https://devcenter.kinvey.com/nodejs/guides/flex-services) are lightweight Node microservices used to integrate data and functional business logic into your application. You just need to install and require the modules like you would in any of your Node apps. We like to keep you in your comfort zone aka productive. You can check out this article on [Getting Started with Kinvey FlexServices](https://www.progress.com/blogs/getting-started-with-kinvey-flexservices) to learn more.

## Microservice Architecture
One of the benefits of Node is the ability to keep you code scalable and modularized. This lends itself to building out microservices that allow you to have a "single responsibility" type building model for your application. That is to say, one app that does one job. This makes scalability and organization of you overall application much more manageable. Instead of worrying about breaking your billing logic because you wanted to change part of you inventory process, you separate them into individual services and leave that stress for another day.

![kinvey microservices]((https://d117h1jjiq768j.cloudfront.net/images/default-source/products/kinvey/__SA_Microservices-min.png)

The Kinvey team realized the benefits of this as well and developed the [Kinvey Microservice Framework](https://devcenter.kinvey.com/rest/guides/mobile-microservices-framework) for building, deploying and maintaining scalable microservices. We also take some of the infrastructure work off your hands but autoscaling to the highest degree on out serverless cloud platform. That way you don't have to spend time configuring or developing low-level code with infrastructure providers. You have the option of creating low to no-code microservices using our RapidServices and FlexServices like RapidAuth and RapidData.

## RapidAuth and RapidData
The RapidAuth and [RapidData](https://devcenter.kinvey.com/rest/guides/rapid-data) services Kinvey provides allow you to easily hook up authorization and data integrations with no code. An old manager of mine used to joke that we all had a finite amount of keystroked in our life time ([in case you wonder what yours was](https://keysleft.com/)), so we wanted to help you out by giving you less code to write 🤗. Sure, I kid, but I have never found coding up these integrations to be quick or painless job. RapidAuth is pretty much what it sounds like: getting users authenticated rapidly. We do this with our [Mobile Identity Connenct](https://devcenter.kinvey.com/rest/guides/mobile-identity-connect) service which connects your app to enterprise identity and single sign=on solutions. We use OAuth2 as an underlying identity protocol for authentication and redirect users as necessary. There are many options to work with MIC including: SAML, OAuth2, OpenID Connect, Active Directory, LDAP, SAML-WRAP, Facebook Auth and Custom Authlink. 

![MIC Architecture](https://devcenter.kinvey.com/guides/mobile-identity-connect/authlink-architecture.png)
![kinvey MIC configuration](https://devcenter.kinvey.com/guides/mobile-identity-connect/oauth2.png)

The [RapidData](https://devcenter.kinvey.com/rest/guides/rapid-data) service lets you use integrations like SAP, Salesforce, Sharepoint, NoSQL and Rest APIs to feed data into your applications instead of having to develop or deploy complex APIs.

![sql service image](https://devcenter.kinvey.com/rest/guides/rapid-data/sqlso.png)

## CLI
Practically every framework out there today has a Command Line Interface tool, because they're awesome, duh. Of course, it is also handy that most of our code editors have bash integration so that we don't have to switch from screen to screen or coding to GUI in order to run commands for our application. Kinvey is right there with you. Our [CLI](https://github.com/Kinvey/kinvey-cli) tool lets you work with your FlexServices, business logic, applications, app environments, and collections all through CLI commands. Our team is constantly updating the CLI to help it help you 😉 check out the [changelog](https://github.com/kinvey/kinvey-cli/blob/HEAD/CHANGELOG.md) to keep up-to-date with all the newness.

- *CI/CD integration with the CLI*

## Some Extra Goodies
I wanted to make a shout-out to a few other features Kinvey offers that aren't _eactly_ Node-centric but are great especially for creating multi-channel applications. 
### Built-in Security
Security is tricky, especially when it comes to mobile devices. 

### Data Acceleration with Offline 
Although, we as users are more connected than ever these days, our _network_ connections aren't always the most reliable. 
- Offline Cloud Caching
- Offline sync built into the SDK

## Your Turn 👩🏽‍💻
I hope I gave you a good view into some of the benefits that Kinvey brings to Node developers. The goal is to help you create native apps across multiple platforms quickly and easily while still being in control. As Node developer ourselves, our team knows where nuisances lay in the coding processes. We try to take care of those nuisances for you so you can work on your actual product and release features your users are asking for. Check out more information at [kinvey.com](https://www.progress.com/kinvey) or jump right in to some docs and tutorials at our [devcenter](https://devcenter.kinvey.com/nodejs/tutorials). Feel free to [reach out to us](https://www.progress.com/kinvey/contact) if you have any questions or want more info. Happy coding! 
