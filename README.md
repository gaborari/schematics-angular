# Angular Schematics for Productivity and Consistency

Developing large-scale web-applications is *hard*, and without a lot of
experience building large Angular applications, it's very easy to make
an architectural or structural mistake that could cost your team a lot
of money and time to fix down the road once that mistake is realized.

The schematics in this library will help your team develop Angular
applications that are consistent and have an architecture/folder
structure that will scale for extremely large projects right from the
get-go.

The output of these schematics is based on many years of experience
building large-scale projects in Angular, and have been used in
applications that contain several hundred-thousand lines of code. Thus,
the opinions and ideas behind these schematics have been battle-tested
and proved to prevent and solve scalability problems many people run
into when building large-scale Angular projects.

## Installation

To add these schematics to your angular-cli project, type the
following in the console at the root of your project:

```bash
npm install @egervari/schematics-angular --save-dev
```

To run schematics from your console, also add the following global
npm library:

```bash
npm install -g @angular-devkit/schematics-cli
```

### Using Schematics Via Console

#### Adding prettier and overwriting TSLint and Prettier rules

To add prettier (if you currently don't have it installed) and use
Rangle's preferred starting point for TSLint and Prettier rules, run
the following schematic from your console:

```bash
schematics @egervari/schematics-angular:tslint-and-prettier
```

Running this schematic will also create a bunch of scripts to
conveniently check and fix your project so you don't have to add them
yourself.

You should see the following updates to your project:

```bash
    Added "prettier" into devDependencies
    Added "tslint-config-prettier" into devDependencies
CREATE /prettier.config.js (173 bytes)
UPDATE /tslint.json (869 bytes)
UPDATE /package.json (2552 bytes)
```

#### Creating Features

To create a feature module containing components, routes, services,
types and isolated ngrx infrastructure, you must specify the feature's
`name`, `path` and optionally, you can specify your project's component
`prefix` for its selector, but the schematic can often figure this out
from your Angular project workspace.

```bash
schematics @egervari/schematics-angular:feature --name=my-feature --path=src/app --prefix=rng
```

If your project currently does not have a `/features` folder, the
schematic will create one for you.

You should see the following files be created/updated when running this
schematic:

```bash
CREATE /src/app/features/my-feature/my-feature-routing.module.ts (370 bytes)
CREATE /src/app/features/my-feature/my-feature.module.ts (676 bytes)
CREATE /src/app/features/my-feature/components/my-feature/my-feature.component.html (0 bytes)
CREATE /src/app/features/my-feature/components/my-feature/my-feature.component.scss (12 bytes)
CREATE /src/app/features/my-feature/components/my-feature/my-feature.component.ts (224 bytes)
CREATE /src/app/features/my-feature/components/index.ts (52 bytes)
CREATE /src/app/features/my-feature/services/my-feature.service.ts (200 bytes)
CREATE /src/app/features/my-feature/store/my-feature.actions.ts (239 bytes)
CREATE /src/app/features/my-feature/store/my-feature.effects.ts (453 bytes)
CREATE /src/app/features/my-feature/store/my-feature.reducer.ts (560 bytes)
CREATE /src/app/features/my-feature/store/my-feature.store.ts (305 bytes)
CREATE /src/app/features/my-feature/types/my-feature-state/my-feature-state.functions.spec.ts (419 bytes)
CREATE /src/app/features/my-feature/types/my-feature-state/my-feature-state.functions.ts (158 bytes)
CREATE /src/app/features/my-feature/types/my-feature-state/my-feature-state.interface.ts (56 bytes)
UPDATE /src/app/store/app.reducer.ts (543 bytes)
UPDATE /src/app/types/app-state/app-state.interface.ts (175 bytes)
UPDATE /src/app/types/app-state/app-state.functions.ts (273 bytes)
UPDATE /src/app/app-routing.module.ts (355 bytes)
```

#### Creating Modules

Sometimes you wish to create modules outside of your routes. They are
not really features, but reusable pieces of code the rest of the app
can share. To create such a module, run the following schematic:

```bash
schematics @egervari/schematics-angular:module --name=my-module --path=src/app
```

If your project currently does not have a `/modules` folder, the
schematic will create one for you.

You should see the following files be created/updated when running this
schematic:

```bash
CREATE /src/app/modules/my-module/my-module.module.ts (559 bytes)
CREATE /src/app/modules/my-module/services/my-module.service.ts (199 bytes)
CREATE /src/app/modules/my-module/store/my-module.actions.ts (236 bytes)
CREATE /src/app/modules/my-module/store/my-module.effects.ts (448 bytes)
CREATE /src/app/modules/my-module/store/my-module.reducer.ts (547 bytes)
CREATE /src/app/modules/my-module/store/my-module.store.ts (303 bytes)
CREATE /src/app/modules/my-module/types/my-module-state/my-module-state.functions.spec.ts (410 bytes)
CREATE /src/app/modules/my-module/types/my-module-state/my-module-state.functions.ts (154 bytes)
CREATE /src/app/modules/my-module/types/my-module-state/my-module-state.interface.ts (55 bytes)
UPDATE /src/app/store/app.reducer.ts (660 bytes)
UPDATE /src/app/types/app-state/app-state.interface.ts (314 bytes)
UPDATE /src/app/types/app-state/app-state.functions.ts (425 bytes)
UPDATE /src/app/app.module.ts (768 bytes)
```

#### Creating Components

Creating components is equally easy - make sure to point the `path`
to the module/feature folder you wish the component to be located:

```bash
schematics @egervari/schematics-angular:component --name=my-form --path=src/app
```

If your path currently does not have a `/components` folder, the
schematic will create one for you.

You should see the following files be created/updated when running this
schematic:

```bash
CREATE /src/app/components/my-form/my-form.component.html (0 bytes)
CREATE /src/app/components/my-form/my-form.component.scss (12 bytes)
CREATE /src/app/components/my-form/my-form.component.ts (214 bytes)
UPDATE /src/app/components/index.ts (192 bytes)
UPDATE /src/app/app.module.ts (2484 bytes)
```

#### Creating Services

Creates a service and updates the containing module file.

```bash
schematics @egervari/schematics-angular:service --name=my-api --path=src/app
```

If your path currently does not have a `/services` folder, the
schematic will create one for you.

You should see the following files be created/updated when running this
schematic:

```bash
CREATE /src/app/services/my-api.service.ts (200 bytes)
UPDATE /src/app/app.module.ts (2561 bytes)
```

#### Creating Types

Creates a paired interface and functions file for a given model.

```bash
schematics @egervari/schematics-angular:type --name=user-profile --path=src/app
```

If your path currently does not have a `/types` folder, the
schematic will create one for you.

You should see the following files be created when running this
schematic:

```bash
CREATE /src/app/types/user-profile/user-profile.functions.spec.ts (390 bytes)
CREATE /src/app/types/user-profile/user-profile.functions.ts (146 bytes)
CREATE /src/app/types/user-profile/user-profile.interface.ts (55 bytes)
```

#### Creating a new project

The Angular CLI and the default @ngrx schematics do not create folders
and files that help developers scale over the long term. Thus, we also
provide a schematic to make some adjustments to a newly created Angular
CLI project to help you get started on the right foot and to support the
other schematics.

To create a new Angular CLI Project, execute the following commands
and you're good to go:

```bash
npm install @angular/cli -g

ng new my-project
```

When asked:

* Say **(Y)es** to add Angular Routing
* Select **SCSS** for your stylesheet format

```bash
cd my-project

ng add @ngrx/store
ng add @ngrx/effects

npm install @egervari/schematics-angular --save-dev
```

And then to correct the default structure, run the `initialize`
schematic with no parameters:

```bash
schematics @egervari/schematics-angular:initialize
```

You should see the following changes:

```bash
            Added "prettier" into devDependencies
            Added "tslint-config-prettier" into devDependencies
DELETE /src/app/app.component.html
DELETE /src/app/app.component.scss
DELETE /src/app/app.component.ts
DELETE /src/app/reducers/index.ts
DELETE /src/app/app.effects.ts
DELETE /src/app/app.component.spec.ts
DELETE /src/app/app.effects.spec.ts
CREATE /prettier.config.js (163 bytes)
CREATE /src/app/types/app-state/app-state.functions.ts (118 bytes)
CREATE /src/app/types/app-state/app-state.interface.ts (33 bytes)
CREATE /src/app/components/index.ts (35 bytes)
CREATE /src/app/components/app/app.component.html (1173 bytes)
CREATE /src/app/components/app/app.component.scss (0 bytes)
CREATE /src/app/components/app/app.component.ts (215 bytes)
CREATE /src/app/store/app.reducer.ts (403 bytes)
CREATE /src/app/store/app.effects.ts (180 bytes)
CREATE /src/app/store/app.store.ts (385 bytes)
UPDATE /tslint.json (826 bytes)
UPDATE /package.json (1784 bytes)
UPDATE /src/app/app.module.ts (740 bytes)
```

#### Where to go from here?

From here, you can run schematics for creating features to get your
project started. For example, to create a `landing` section for your
application, run the following schematic:

```bash
schematics @egervari/schematics-angular:feature --name=landing --path=src/app
```

And to create the `home`, `login` and `forgot-password` sections within the
landing module, run the following 3 schematics:

```bash
schematics @egervari/schematics-angular:feature --name=home --path=src/app/features/landing
schematics @egervari/schematics-angular:feature --name=login --path=src/app/features/landing
schematics @egervari/schematics-angular:feature --name=forgot-password --path=src/app/features/landing
```

At this point, take a quick look at your source code and you'll be
astounded as to how much manual labour was saved as a result of using
these schematics. Everything is modularized and chained together for
you, such as your routes, lazy-loading, states, state default values and
reducers. Your NgModule's are properly connected. You have clear
separation of concerns everywhere.

And if you're new to Angular and didn't know the right way to begin
your first project architecturally, this will put you on the right path
to having a great, scalable architecture over the long-term.

### Using Schematics Through WebStorm

To use schematics in WebStorm, right-click on a folder, select
**'New'**, then select **'Angular Schematic'**, and then select any
schematic from the following list:

![alt text](docs/webstorm-1.png "Angular Schematics Selection")

For the parameters input, WebStorm will pass many of the options - such
as project name and path - on your behalf, so all you have to do is set
the `name` parameter for most schematics and you're all set:

![alt text](docs/webstorm-2.png "Add name parameter")

## Building and testing

To build the source code, run:

```bash
npm run build
```

After the schematics are built, to run them locally from the project
root, run:

```bash
cd dist
schematics .:feature --name=app --path=src/app
```

## Linting and Prettier

To clean up the source code, run:

```bash
npm run fix
```

## Publishing

To publish this to npm, run the following commands:

```bash
npm version major/minor/patch
npm run build
npm run publish
```

### Quickly create a patch version

To quickly create a patch version, instead of going through all of the
build and publish commands manually, instead run:

```bash
npm run release-patch
```
