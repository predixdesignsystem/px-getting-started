# Getting started

This is interim documentation for PX-design. It is based on the [getting-started](https://github.com/inuitcss/getting-started) documentation for inuitcss, which PX-design is built on.

## What is PX-design?

PX-design is a collection of Sass-based repos under the PredixDev org on [Github](https://github.com/). PX-design is built on the [inuitcss](https://github.com/inuitcss) framework. We have added functionality to inuitcss and customized some of its existing methodologies but have attempted to remain faithful to inuitcss' core principles.

## What is inuitcss?

inuitcss is a powerful, [Sass](http://sass-lang.com)-based, [BEM](https://en.bem.info), [OOCSS](http://www.slideshare.net/stubbornella/object-oriented-css) framework designed with scalability and performance in mind.

inuitcss provides a solid architectural foundation upon which you can build any size or style of website or app. inuitcss
is what you make of it--it helps you get started, and then gets out of your way.

inuitcss is a framework in its truest sense. It is not a UI Toolkit, with opinionated views on design; it is not one giant download, with hundreds of unnecessary lines of CSS; it is not a 1001-UI-components-plus-the-kitchen-sink, with loads of bloated rules. It is a collection of tiny, composable, configurable, interdependent modules that you can piece together how you want to, when you want to. inuitcss' focus is less upon the actual code within it, but upon the principles of a solid, scalable CSS architecture.

## Management

PX-design, like inuitcss, uses Bower for dependency management. Each px-_reponame_-design repository's `bower.json` will list the other px-_reponame_-design repos required for successful compilation of the Sass contained in the "parent" repository. Each file required by Sass for successful compilation will be shown as a series of `@import` declarations.

The px-_reponame_-design repos are deliberately granular. Developers can consume as many or as few as they require. There are also "meta" PX-design repos which are essentially collections of PX-design repos organized along common lines e.g. lists, buttons etc that will provide expediency over granularity.

## As quick as possible

The quickest, simplest way to get started with PX-design is via the [Starter Kit](https://github.com/PredixDev/px-starter-kit-design). Simply run

    $ bower install --save git://github.com/PredixDev/px-starter-kit-design.git

...to grab the correct dependencies, and then import them into this base Sass file:

    // Settings
    @import "px-colors-design/_settings.colors.scss";

    // Generic
    @import "px-normalize-design/_generic.normalize.scss";
    @import "px-box-sizing-design/_generic.box-sizing.scss";
    @import "px-helpers-design/_generic.helpers.scss";

    // Base
    @import "px-flexbox-design/_base.flexbox.scss";
    @import "px-viewport-design/_base.viewport.scss";
    @import "px-typography-design/_base.typography.scss";

    // Trumps
    @import "inuit-clearfix/_trumps.clearfix.scss";
    @import "px-spacing-responsive-design/_trumps.spacing-responsive.scss";
    @import "px-widths-responsive-design/_trumps.widths-responsive.scss";

This source order is imperative, and underpins the entire PX-design framework.

## Setting up a project

With PX-design, you are in charge of almost everything; this includes your master Sass file.

You will need to create your own master Sass file, e.g. `px.scss`, and `@import` yours and PX-design's modules into that. This kind of architecture allows you to intersperse PX-design Sass with your own, whereas most other CSS Frameworks and UI Toolkits only permit you to work before or after you've imported them. This is a perfectly valid (example) setup in PX-design:

    // Settings
    @import "px-defaults-design/_settings.defaults.scss";
    @import "px-colors-design/_settings.colors.scss";
    @import "inuit-responsive-settings/_settings.responsive.scss";
    
    // Tools
    @import "px-functions-design/_tools.functions.scss";
    @import "px-mixins-design/_tools.mixins.scss";
    @import "inuit-responsive-tools/_tools.responsive.scss";
    
    // Generic
    @import "px-normalize-design/_generic.normalize.scss";
    @import "px-box-sizing-design/_generic.box-sizing.scss";
    @import "px-helpers-design/_generic.helpers.scss";
    
    // Base
    @import "px-viewport-design/_base.viewport.scss";
    @import "px-typography-design/_base.typography.scss";
    
    // Meta
    @import "px-meta-lists-design/_meta.lists.scss";
    
    // Objects
    @import "px-buttons-design/_objects.buttons.scss";
    @import "px-layout-design/_objects.layout.scss";
    @import "px-box-design/_objects.box.scss";
    
    // Components
    @import "px-some-web-component.scss";

    // Trumps
    @import "px-widths-responsive-design/_trumps.widths-responsive.scss";
    @import "px-spacing-responsive-design/_trumps.spacing-responsive.scss";

## Import order

Because PX-design is broken apart into lots of small, composable modules, it is important that you as the developer piece things together in the correct order. That order is:

* **Settings:** Global variables, site-wide settings, config switches, etc.
* **Tools:** Site-wide mixins and functions.
* **Generic:** Low-specificity, far-reaching rulesets (e.g. normalize.css).
* **Base:** Unclassed HTML elements (e.g. `a {}`, `blockquote {}`, `address {}`).
* **Meta:** Shortcut libraries with collections of objects (e.g. meta-lists, meta-buttons).
* **Objects:** Objects, abstractions, and design patterns (e.g. `.media {}`).
* **Components:** Discrete, complete chunks of UI (e.g. `.carousel {}`).
* **Trumps:** High-specificity, very explicit selectors. Overrides and helper classes (e.g. `.hidden {}`).

The order of partials within each layer is fairly open; it is the sections themselves that are important to get in the correct order.

**N.B.** All partials—including your own—follow the `<section>.<file>` naming convention, e.g. `_objects.box.scss`, `_components.navbar.scss`.

## Core functionality

There are very few **required** PX-design and inuitcss modules, and the ones that are, deal only with config and tooling.

Before it can do anything, PX-design needs to know your base `font-size` and `line-height`. These settings are stored in PX-design's `settings.defaults` file (as `$inuit-base-font-size` and `$inuit-base-line-height`), and can be overridden in the same way you'd [override any of PX-design's config](https://github.com/PredixDev/px-getting-started#modifying-px).

Probably the most opinionated thing PX-design will ever do is reassign your `$inuit-base-line-height` variable to `$inuit-base-spacing-unit`. This value then becomes the cornerstone of your UI, acting as the default (remember, you can override everything in PX-design or inuitcss) margin and padding value for any components that require it.

While this might seem overly opinionated, it does mean that:

1. **You get a free vertical rhythm** because everything sits on a multiple of your baseline, and...
2. **We reduce the amount of [magic numbers](http://csswizardry.com/2012/11/code-smells-in-css/#magic-numbers) in our codebase** because we can rationalise where the majority of values in our CSS came from.

Almost all PX-design modules also require `tools.functions` (see "import-once" functionality above), which is a very simple file containing the import-once function and a handful of math helper functions. These are used to quickly create size variants of objects, e.g. `padding: double($inuit-base-spacing-unit);`, and generate `rem` values from `pixels`.

The other likely piece of required functionality is the `tools.mixins` module. These contain simple font-related mixins that are used later on in certain type-based modules.

Aside from that, most PX-design partials have very few interdependencies, and those that do are all dependency managed via Bower.

## Installing new modules

Installing new modules via Bower is simple; just refer to the module's GitHub repository's README for the specific command.

Almost all of PX-design's modules depend on [px-default-design](https://github.com/PredixDev/px-default-design) and [px-functions-design](https://github.com/PredixDev/px-functions-design). If you are using Bower then you will get these installed automatically.

## Modifying PX-design

PX-design's Sass is highly configurable, but **should not be edited directly**. The correct way to make changes to PX-design is to pass in variables **before** you `@import` the specific file. Let's take [px-default-design](https://github.com/PredixDev/px-default-design) as an example--in this file we can see the variables `$inuit-base-font-size` and `$inuit-base-line-height`. If we want to keep these as-is then we needn't do
anything other than `@import` the file. If we wanted to change these values to `12px` and `18px` respectively (don't worry, inuitcss will convert these pixel values to rems for you) then we just need to pass those values in before the
`@import`, thus:

    $inuit-base-font-size:   12px;
    $inuit-base-line-height: 18px;
    @import "px-defaults-design/_settings.defaults.scss";

The same goes for any PX-design or inuitcss module; you can configure it by predefining any of its variables immediately before the `@import`:

    $inuit-btn-background:      rgb(247,247,247);
    $inuit-btn-color:           rgb(47,47,47);
    $inuit-enable-btn--full:    true;
    @import "px-buttons-design/_objects.buttons.scss";

    $inuit-enable-layout--middle:   true;
    @import "px-layout-design/_objects.layout.scss";

    $inuit-enable-flag--rev:        true;
    $inuit-enable-flag--responsive: true;
    @import "px-flag-design/_objects.flag.scss";

This method of modifying the framework means that you don't need to edit any files directly (thus making it easier to update the framework), but also means that you're not left with huge, bloated, monolithic variables files from which
you need to configure an entire library.

## Off by default

In the interests of reducing the amount of code in your project, all of PX-design's module-variants are turned off by default. This gives PX-design two layers of reduced bloat:

1. **You only include the specific files you need**, so you're immediately starting with a very trimmed down codebase.
2. **Any variants are switched off by default**, so if you _just_ want buttons, you don't get every different size and permutation of them unless you explicitly tell PX-design you want them.

To turn features on, just set their switches to true (again, _before_ you `@import` the file):

    $inuit-enable-btn--full:    true;
    $inuit-enable-btn--large:   true;
    @import "px-buttons-design/_objects.buttons.scss";

## Extending PX-design

Two things about PX-design make it very extensible. Firstly, it is a framework in its truest sense; it is designed to lay an unopinionated foundation upon which _you_ do the majority of the work. Secondly, scalability is one of PX-design's core principles, so it is designed to get larger over time.

Extending PX-design is made very simple because of its very decoupled nature. As opposed to having a monolithic framework which acts as one giant black box, you can add your own functionality in and around PX-design code. This means that you can grow your codebase in any direction from any point. PX-design has some default tooling, but there's no reason you cannot create your own tools partials, there is no reason why you couldn't add some of your own objects that PX-design doesn't have.

To extend PX-design, simply create a partial in the `<section>.<file>` format, and `@import` it wherever it is needed.

### Known issues

1. @import paths won't resolve in an IDE/editor unless you add bower_components/[some dir or *] as a resource root for your IDE/editor. Note that such paths resolve correctly at compile time due to the use of `node-sass-import-once` during our grunt-sass compilation.
