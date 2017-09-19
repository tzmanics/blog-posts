# Angular CLI Cheat Sheet from Kendo UI
I am a big fan of the [Angular CLI](https://cli.angular.io/) because it makes it really easy to spin up a new Angular project and start customizing how it is built. Whenever I start a new Angular project, I immediately create the skeleton with ng new adding flags to for what version of Angular and what style library I want to use, then I start installing the [Kendo UI for Angular theme](http://www.telerik.com/kendo-angular-ui/components/styling/) and [components](http://www.telerik.com/kendo-angular-ui/components/) I need, then serve it up.

```bash
ng new awesome-new-project --ng4 --style sass
cd awesome-new-project
npm install @progress/kendo-theme-bootstrap @progress/kendo-angular-charts @progress/kendo-angular-intl @progress/kendo-angular-l10n @progress/kendo-drawing hammerjs @angular/animations
ng serve --live-reload --watch
```

I like this because then I’ve done everything, in the foreseeable future, that I need to do in the command line and I can open my code editor and get to work. Since I ran ng serve with the live-reload flag, every time there is a change my project will re-build and re-load the web server.

There are many great resources for digging into everything that the CLI provides you, like the Angular CLI Wiki page, but I’ve always wanted something quicker. I decided to put together a cheat sheet that allows you to quickly scroll through all the available CLI commands with their options and flags.

## Cheat Sheet Key

The format for the cheat sheet has the CLI Command listed first along with its aliases, if they exist, in parenthesis next to it. Then there is a description of what the command does, where you can use the command and, if there are options to use with that command, the options are listed.

---
# Command: `e2e (-e)`
## Description
Run e2e tests in existing project.
## Works
Inside Project
---

Here with end-to-end testing, or e2e, we see that we can either run it as 
`ng e2e`
or
`ng e`
This will run any existing e2e tests that exist in the project when we run it from inside the project directory.

Below that the command’s flags are listed. These basically let us customize how or when commands are run.

---
## Flags
---
### `config (-c)`
#### Type
`String`
#### Description
Use a specific config file. Defaults to the protractor config file in `.angular-cli.json`.
#### Example
`ng e2e --config tests/configs/e2e.json`
`ng e -c tests/configs/e2e.json`
---

Each flag will be listed followed by its alias in parenthesis if it has one. Then the Type will tell you what you can pass the flag. For instance, here we know we need to pass a string but some flags require Booleans or arrays. After that, the flag’s description is listed and an example of how you may use the command and flag.

I hope you find this cheat sheet handy in helping you build your Angular apps. If you’re a fan of building robust Angular apps faster, check out some of our Kendo UI Components and tools:
- [Build Native Angular Components Fast](http://www.telerik.com/kendo-angular-ui/components/)
- [Progress Theme Builder](http://themebuilder.telerik.com/kendo-angular-ui)
- [Blog Posts & Tutorials](https://developer.telerik.com/)

Happy Coding!

# Command: `build`
## Description
Compiles the application into an output directory, stored inside the `dist` directory.
## Flags
---
###  `--aot`
#### Description
Build using Ahead of Time compilation.
#### Type
`Boolean`
#### Examples
`ng build --aot`

### `--app (-a)`
#### Description
Specifies app name to use.
#### Type
`String`
#### Examples
`ng build --app test`
`ng build -a staging`

### `--base-href (-bh)`
#### Description
Base url for the application being built.
#### Type
`String`
#### Examples
`ng build --base-href http://test-staging.com`
`ng build -bh test-staging.com`

#### `--deploy-url (-d)`
#### Description
URL where files will be deployed.
#### Type
`String`
#### Examples
`ng build --deploy-url http://test-staging.com`
`ng build -d test-staging.com`

### `--environment (-e)`
#### Description
Defines the build environment.
#### Type
`String`
#### Examples
`ng build --environment prod`
`ng build -e dev`

### `--extract-css (-ec)`
#### Description
Extract css from global styles onto css files instead of js ones.
#### Type
`Boolean`
#### Examples
`ng build --extract-css`
`ng build -ec`

### `--i18n-file`
#### Description
Localization file to use for i18n.
#### Type
`String`
#### Examples
`ng build --i18n-file myi18n.json --i18n-format json --locale de`

### `--i18n-format`
#### Description
Format of the localization file specified with --i18n-file.
#### Type
`String`
#### Examples
`ng build --i18n-file myi18n.json --i18n-format json --locale de`

### `--locale`,
#### Description
Locale to use for i18n.
#### Type
`String`
#### Examples
`ng build --i18n-file myi18n.json --i18n-format json --locale de`

### `--missing-translation`,
#### Description
How to handle missing translations for i18n.
#### Type
`String`
#### Options
`error`, `warning`, `ignore`
#### Examples
`ng build --missing-translation warning`

### `--output-hashing (-oh)`
#### Description
Define the output filename cache-busting hashing mode.
#### Type
`String`
#### Options 
`none`, `all`, `media`, `bundles`
#### Examples
`ng build --output-hashing bundles`
`ng build -oh all`

### `--target (-t)`
#### Description
Defines the build target.
#### Type
`String`
### Options
`development (dev)`, `production (prod)`
#### Default
`development`
#### Examples
`ng build --target=development`
`ng build --prod`

### `--output-path (-op)`
#### Description
Path where output will be placed.
#### Type
`Path`

### `--sourcemaps (--sm, --sourcemap)`
#### Description
Output sourcemaps.
#### Type
`Boolean`

### `--vendor-chunk (-vc)`
#### Description
Use a separate bundle containing only vendor libraries.
#### Type
`Boolean`
#### Default
`true`
#### Examples
`ng build --vendor-chunk=false`

### `--verbose (-v)`
#### Description
Adds more details to output logging.
#### Type
`Boolean`
#### Default
`false`

### `--progress (-pr)`
### Description
Log progress to the console while building.
#### Type
`Boolean`
#### Default
`true`

### `--watch (-w)`
#### Description
Run build when files change.
#### Type
`Boolean`
### Default
`false`

### `--poll`
#### Description
Enable and define the file watching poll time period (milliseconds).
#### Type
`Number`
#### Default
`pollDefault`

# Command: `completion`
## Description
Adds autocomplete functionality to `ng` commands and subcommands.
## Works
Everywhere
## Flags
---
### `all (-a)`
#### Description:
Generate a completion script compatible with both bash and zsh.
#### Type
`Boolean`
#### Default
`true`

### `bash (-b)`
#### Description
Generate a completion script for bash.
#### Type
`Boolean`
#### Default
`false`

### `zsh (-z)`
#### Type
`Boolean`
#### Default
`false`

---

# Command: `doc`
## Description
Opens the official Angular documentation for a given keyword on [angular.io](https://angular.io/).
## Works
everywhere
## Flags
---
### `search (-s)`
#### Type
`String`
#### Default
`false`
#### Example
`ng doc --search=doc`

---

# Command: `e2e (-e)`
## Description
Run e2e tests in existing project.
## Works
Inside Project
## Flags
---
### `config (-c)`
#### Type
`String`
#### Description
Use a specific config file. Defaults to the protractor config file in `.angular-cli.json`.
#### Example
`ng e2e --config tests/configs/e2e.json`
`ng e -c tests/configs/e2e.json`

### `specs (-sp)`
#### Type
`Array`
#### Default
`[]`
#### Description
common_tags_1.oneLine
Override specs in the protractor config.
Can send in multiple specs by repeating flag (ng e2e --specs=spec1.ts --specs=spec2.ts).

### `element-explorer (-ee)`
#### Description
Start Protractor\'s Element Explorer for debugging.
#### Type
`Boolean`
#### Default
`false`

### `webdriver-update (-wu)`
#### Description
Try to update webdriver.
#### Type
`Boolean`
#### Default
`true`

### `serve (-s)`
#### Description
common_tags_1.oneLine 
Compile and Serve the app.
All non-reload related serve options are also available (e.g. --port=4400).
#### Type
`Boolean`
#### Default
`true`

### `port`
#### Description
The port to use to serve the application.
#### Default
`0`

### `watch`
#### Description
Run build when files change.
#### Default
`false`

---
# Command: `eject`
## Description
Ejects your app and output the proper webpack configuration and scripts.
## Flags
---
### `--force`
#### Type
`Boolean`
#### Description
Overwrite any webpack.config.js and npm scripts already existing.

### `--app (-a)`
#### Description
Specifies app name to use.
#### Type
`String`

---
# Command: `generate`
## Flags
---
blueprints: blueprints,
 const aliasMap = {
    'cl': 'class',
    'c': 'component',
    'd': 'directive',
    'e': 'enum',
    'g': 'guard',
    'i': 'interface',
    'm': 'module',
    'p': 'pipe',
    'r': 'route',
    's': 'service'
}

---
# Command: `get`
## Description
Get a value from the configuration.
## Works
Everywhere
## Flags
---
### `--global`
#### Type
`Boolean`
#### Default
`false`
#### Description
Get the value in the global configuration (in your home directory).
 
---
# Command: `help`
## Description
Shows help for the CLI.
## Works
Everywhere
## Flags:
---
anonymousOptions: ['command-name (Default: all)'],
 
---
# Command: `init`
## Description
Creates a new Angular CLI project in the current folder.
## Works
Everywhere
## Flags
---
### `--dry-run (-d)`
#### Type
`Boolean`
#### Default
`false`

### `--verbose (-v)`
#### Type
`Boolean`
#### Default
`false`

### `--link-cli (-lc)`
#### Type
`Boolean`
#### Default
`false`

### `--ng4`
#### Type
`Boolean`
#### Default
`false`

### `--skip-install (-si)`
#### Type
`Boolean`
#### Default
`false`

### `--skip-git (-sg)`
#### Type
`Boolean`
#### Default
`false`

### `--skip-tests (-st)`
#### Type
`Boolean`
#### Default
`false`

### `--skip-commit (-sc)`
#### Type
`Boolean`
#### Default
`false`

### `--name (-n)`
#### Type
`String`

### `--source-dir (-sd)`
#### Type
`String`
#### Default
`src`

### `--style`
#### Type
`String`
#### Default
`css`

### `--prefix (-p)`
#### Type
`String`
#### Default
`app`

### `--routing`
#### Type
`Boolean`
#### Default
`false`

### `--inline-style (-is)`
#### Type
`Boolean`
#### Default
`false`

### `--inline-template (-it)`
#### Type
`Boolean`
#### Default
`false`

--- 
# Command: `lint (l)`
## Description
Lints code in existing project.
## Works
Inside Project
## Flags
---
### `fix`
#### Description
Fixes linting errors (may overwrite linted files).
#### Type
`Boolean`
#### Default
`false`

### `--force`
#### Description
Succeeds even if there was linting errors.
#### Type
`Boolean`
#### Default
`false`

### `--format (-t)`
#### Description
common_tags_1.oneLine
#### Type
`String`
### Options
`prose`, `json`, `stylish`, `verbose`, `pmd`, `msbuild`, `checkstyle`, `vso`, `fileslist`
#### Default
`prose`

---    
# Command: `new`
## Description
Creates a new directory and a new Angular app.
## Works: 
Outside of project
## Flags
---
### `--dry-run (-d)`,
#### Description
Run through without making any changes.
#### Type
`Boolean`
#### Default
`false`

### `--verbose (-v)`
#### Description
Adds more details to output logging.
#### Type
`Boolean`
#### Default
`false`

### `--link-cli (-lc)`
#### Description
Automatically link the `@angular/cli` package.
#### Type
`Boolean`
#### Default
`false`

### `--ng4`
#### Description
Create a project with Angular 4 in the template.
#### Type
`Boolean`
#### Default
`false`
#### Examples
`ng new test-project --ng4`

### `--skip-install (-si)`
#### Description
Skip installing packages.
#### Type
`Boolean`
#### Default
`false`
#### Examples
`ng new test-project --skip-install`
`ng new test-project -si`

### `--skip-git (-sg)`
#### Description
Skip initializing a git repository.
#### Type
`Boolean`
#### Default
`false`

### `--skip-tests (-st)`
#### Description
Skip creating spec files.
#### Type
`Boolean`
#### Default
`false`

### `--skip-commit (-sc)`
#### Description
Skip committing the first commit to git.
#### Type
`Boolean`
#### Default
`false`

### `--directory (-dir)`
#### Description
The directory name to create the app in.'
#### Type
`String`

### `--source-dir (-sd)`
#### Description
The name of the source directory.
#### Type
`String`
#### Default
`src`

### `--style`
#### Description
The style file default extension.
#### Type
`String`
#### Default
`css`

### `--prefix (-p)`
#### Description
The prefix to use for all component selectors.
#### Type
`String`
#### Default
`app`

### `--routing`
#### Description
Generate a routing module.
#### Type
`Boolean`
#### Default
`false`

### `--inline-style (-is)`
#### Description
Should have an inline style.
#### Type
`Boolean`
#### Default
`false`

### `--inline-template (-it)`
#### Description
Should have an inline template.
#### Type
`Boolean`
#### Default
`false`

---
# Command: `serve (server, s)`
## Description
Builds and serves your app, rebuilding on file changes.
## Flags
---
### `--port (-p)`
#### Description
Port to listen to for serving.
#### Type
`Number`
#### Default
`defaultPort`

### `--host (-H)`
#### Description
Listens only on ${defaultHost} by default.
#### Type
`String`
#### Default
`defaultHost`

### `--proxy-config (-pc)`
#### Description
Proxy configuration file.
#### Type
`Path`

### `--ssl`
#### Description
Serve using HTTPS.
#### Type
`Boolean`
#### Default
`defaultSsl`

### `--ssl-key`
#### Description
SSL key to use for serving HTTPS.
#### Type
`String`
#### Default
`defaultSslKey`

### `--ssl-cert`
#### Description
SSL certificate to use for serving HTTPS.
#### Type
`String`
#### Default
`defaultSslCert`

### `--open (-o)`
#### Type
`Boolean`
#### Default
`false`
#### Description
Opens the url in default browser.,

### `--live-reload (-lr)`
#### Description
Whether to reload the page on change, using live-reload.
#### Type
`Boolean`
#### Default
`true`

### `--live-reload-client`
#### Type
`String`
#### Description
Specify the URL that the live reload browser client will use.

### `--hmr`
#### Description
Enable hot module replacement.
#### Type
`Boolean`
#### Default
`false`

### `--watch`
#### Description
Rebuild on change.
#### Default
`true`

---
# Command: `set`
## Description
Set a value in the configuration.
## Works
Everywhere
## Flags
---
### `--global (-g)`
#### Description
Set the value in the global configuration rather than in your project\'s.
#### Type
`Boolean`
#### Default
`false`

---
# Command: `test`
## Flags
---
### `--watch (-w)`
#### Description
Run build when files change.
#### Type
`Boolean`
#### Default
`true`

### `--code-coverage (-cc)`
#### Description
Coverage report will be in the coverage/ directory.
#### Type
`Boolean`
#### Default
`false`

### `--config (-c)`
#### Description
Use a specific config file.
#### Type
`String`
#### Default
To the karma config file in .angular-cli.json.

### `--single-run (-sr)`
#### Description
Run tests a single time.
#### Type
`Boolean`
#### Default
`false`

### `--progress`
#### Description
Log progress to the console while in progress.
#### Type
`Boolean`
#### Default
`true`

### `--browsers`
#### Description
Override which browsers tests are run against.
#### Type
`String`

### `--colors`
#### Description
Enable or disable colors in the output (reporters and logs).
#### Type
`Boolean`

### `--log-level`
#### Description
Level of logging.
#### Type
`String`

### `--port`
#### Description
Port where the web server will be listening.
#### Type
`Number`

### `--reporters`
#### Description
List of reporters to use.
#### Type
`String`

### `--sourcemaps (-sm, -sourcemap)`
#### Description
Output sourcemaps.
#### Type
`Boolean`
#### Default
`true`

### `--poll`
#### Description
Enable and define the file watching poll time period (milliseconds).
#### Type
`Number`
#### Default
`pollDefault`

### `--app (-a)`
#### Description
Specifies app name to use.
#### Type
`String`

---
# Command: `version (v, --version, -v)`
## Description
Outputs Angular CLI version.
## Works
Everywhere
## Flags
---
### `--verbose`
#### Description
Adds more details to output logging.
#### Type
`Boolean`
#### Default
`false`

---     
#Command: `xi18n`
## Description
Extracts i18n messages from source code.
## Works: 'insideProject',
## Flags
---
### `--i18n-format (-f)`,
#### Description
Output format for the generated file.
#### Type
`String`
#### Default
`xlf`
#### Options
`xmb`, `xlf`

### `--output-path (-op)`
#### Description
Path where output will be placed.
#### Type
`Path`
#### Default
`null`

### `--verbose`
#### Description
Adds more details to output logging.
#### Type
`Boolean`
#### Default
`false`

### `--progress`
#### Description
Log progress to the console while running.
#### Type
`Boolean`
#### Default
`true`

### `--app (-a)`
#### Description
Specifies app name to use.
#### Type
`String`

### `--locale (-l)`
#### Description
Specifies the source language of the application.
#### Type
`String`

### `--out-file (-of)`
#### Description
Name of the file to output.
#### Type
`String`
