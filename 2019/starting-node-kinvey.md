# Getting Started with Node & Kinvey
This is a quick post to help you get up and running with a new Node project connected to a Kinvey backend. Let's just jump right in!

## Creating a Node Project
I make a lot of Node projects, some even see the light of day 😛 so I have a script to spin one up. I got the idea from [this tweet](https://twitter.com/bitandbang/status/1082331715471925250) from [Tierney Cyren](https://twitter.com/bitandbang/) and learned even more from [this post](https://philna.sh/blog/2019/01/10/how-to-start-a-node-js-project/) by [Phil Nash](https://twitter.com/philnash).

![picture of Tierney's tweet](https://bit.ly/2OPHMjC)

As the tweet says, in your terminal you can just type:

```
npx license mit > LICENSE
npx gitignore node
npx covgen <your email address>
npm init -y
```

What all is happening here? We're using [`npx`](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) to use an `npm` module whether we have it installed or not. First, [`license`](https://www.npmjs.com/package/license) to generate the MIT license, [`gitignore`](https://www.npmjs.com/search?q=gitignore) to fetch a Node.js `.gitignore` file, and [`covgen`](https://www.npmjs.com/package/covgen) to generate the [Contributor Covenant](https://www.contributor-covenant.org/) inside your project directory using your email as the contact info. Finally, we run `npm init -y` to spin up a `package.json` file for the project. The `-y` or `--yes` flag uses the [defualt values](https://docs.npmjs.com/creating-a-package-json-file#default-values-extracted-from-the-current-directory) or the configs you can set using `npm.set`.

```
npm set init.author.email "example-user@example.com"
npm set init.author.name "example_user"
npm set init.license "MIT"
```

That's it! I now have a shortcut in my `~/.bashrc` file so that I can just type `node-project` in an empty directory and it spins all this up plus initializes `git` in the directory and makes the first initial commit. Nash explains it in-detail in his post I listed above. Here's what my function:

```
function node-project {
  git init
  npx license mit>LICENSE
  npx gitignore node
  npx covgen "$(npm get init.author.email)"
  npm init -y
  git add .
  git commit -m 'initial commit'
}
```

## Connecting to Kinvey
Now that we have out base project we get to connect it to our Kinvey backend.

## Next Steps
We're all setup! Pretty easy, right? What will we do next, such possibilities. Here are some great resources to help you on your coding journey:

