## vs code session

a sticker application

look at different setting and theme control
four spaces?!?!

typescript compiler for javascript, type checking

console output
look at tasks in VSCode
can scroll through tasks

can set breakpoints in gulp tasks

launch.json will tell VSCode how to run that app
prelaunch task to build

?? what does F5 do ??

Can use chrome debugger in Code instead of doing it in the browser.
switch to the terminal decently easy to start your app

This session wasn't what I expected. It was a little hard to follow because there was a lot of jumping around. The speaker knew where he was headed to next but since we were privy there was a bit of catch up needed. He was also using the insiders version of VSCode so we didn't have all the capabilities he had for his demo.

Definitely presumed that we had used Code before.

I thought we would be setting up our Code environment to prepare us to work with applications in azure. Although I learned about more extensions, I had my VSCode opened but didn't have any new insights on what to setup/change or how.

A look into different extensions that exist.

Can right-click a document name in a file to update it.

VSTS can't be setup using azure cli just yet

using containers
create new docker file
Docker extensiion
// recommended extensions is dynamic
added multistage build file
build intermediate stages then pull from that

deploy.azcli
you can create az this filr to make calls to the azure cli
the autocompletes even have subscrition names and give you a thorough list for all of the az cli flags
can set defaults like location and group

az appservice plan create --name <name> --is-linux --sku <which tier>
az webapp create --name <name> --plan <plan>
can also configure documentdb, web app config settings and set variables

intellisense for azure command line tool
commad tick to open up a broswer

# Hidden Gems in Azure Leon Wlicki lwelicki Rajmohan (rajraj)
quickstart tutorials on the portal immediately to hel you get started
a guided tour in the help section, start and stop at any time
added links to documentations on the differenct tabs home screens
context based help buttons, bring the docs to you that they predict you will need
portal.azure.com the production one
preview.portal.com to see the new things coming to the portal
you can change the language in settings, 18 languages available, multiple locations available as well
set up your subscriptions that you want to work with 

global portal search
let's you access recently used resources, then filters results as you type
G/ to get to the search (! No mouse use !)
keyboard shortcutes in the help  menu (woopwoop)
in all resources you can filter and sort with different dropdown menus subscriptions, types, .ocations, grouping

you can multi-select and stop all at once

customize list of column with the columns menu at the top of the service blade
you can add a tag to each resource

in any resource group you can place a lock so that that resources cannot be moved or deleted

custom templates in the main search bar (you see deploy custom template)
can find the github templates right in the custom deployments resource page
if you need to add a storage service you had an add reource button at the top of the blade to quikly add that resource
you can also make a customized template and it makes sure that you add the correct information

your get helpers to run the template with pcli powershell .net ruby

azure cloud shell available at any time in the portal s

public preview azure mobile app
