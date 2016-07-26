# UI Email Ecosystem
*DEG UI Email Code Standards, Design Patterns, Frameworks & Tooling*

## Table of Contents
  1. [Code Style Guide](#code-style-guide)
    - [HTML](#html)
    - [CSS](#css)
  2. [Design Patterns & Considerations](#design-patterns--considerations)
    - [Atomic Design](#atomic-design)
    - [Email Client Support](#email-client-support)
    - [Accessibility](#accessibility)
    - [Performance](#performance)
    - [Detailed Design Patterns & Anti-Patterns](#detailed-design-patterns--anti-patterns)
  3. [Frameworks](#frameworks)
    - [Skeletor](#skeletor)
    - [Pattern Lab](#pattern-lab)
  4. [Libraries](#libraries)
  5. [Tooling](#tooling)
    - [IDEs/Editors](#ides)
    - [CSS](#css-1)
    - [Task Runners](#task-runners)
    - [Visual Editors](#visual-editors)
    - [ALM/Version Control](#alm)
    - [Testing](#testing)

## Code Style Guide

### HTML
**HTML5 doctype**
* HTML5 (HTML syntax) is preferred for all HTML documents.

**Formatting & Syntax**
* Use tabs (4 spaces) for indentation
* Nested elements should be indented once

     __Bad Formatting__
    ```html
    <table cellpadding="0" cellspacing="0">
                <tr>
				<td>
            // ...
            </td>
        </tr></table>
    ```

    __Good Formatting__
    ```html
    <table cellpadding="0" cellspacing="0">
        <tr>
        	<td>
            // ...
        	</td>
        </tr>
    </table>
    ```

* Hybrid Layouts

### CSS
**Organization**
* CSS should be organized into partials and follow DEG's modified Atomic CSS structure of Basics, Components, Templates, & Utilities. These partials will be processed using PostCSS and the available configuration options in Skeletor.

    ```
    css
    |-- basics/
    |   |-- buttons.css
    |   |-- headings.css
    |   |-- ...
    |-- components/
    |-- templates/
    |-- utilities/
    ```

**Formatting**
* Use tabs (4 spaces) for indentation
* When using multiple selectors in a rule declaration, give each selector its own line
* When defining multiple properties, give each property its own line

    __Bad Formatting__
    ```css
    .selector{
            property:value; property:value; }
        .selector, .selector, .selector {
            // ...
        }
        #id {
          // ...
        }
    ```

    __Good Formatting__

    ```css
    .selector {
        property: value;
        property: value;
    }

    .selector,
    .selector,
    .selector {
        // ...
    }
    ```

**Pseudo BEM**
* [BEM](http://getbem.com/) is a CSS methodology and syntax, that helps achieve reusable components. BEM stands for Block Element Modifier and consists of:
    * __Block__: Standalone entity that is meaningful on its own.
    * __Element__: Parts of a block and have no standalone meaning. They are semantically tied to its block.
    * __Modifier__: Flags on blocks or elements. Use them to change appearance or behavior.
* DEG's approach is to follow the general guidelines of BEM and it's syntax, though it is not strictly enforced, which is why it's referred to as Pseudo BEM here and throughout this document. For full documentation on the BEM methodology, reference the [BEM website](http://getbem.com/).

**Variables**
* Use CSS variables for consistancy and maintainablity of styles.
* It is recommended that you use variables for color palettes, font properties, & timing functions. Additional variables may be created on an as needed basis.
* Namespace all variables with `--property-group`.
* Append a logical and easy to reference modifier to all variations: `-modifier`.
* If a logical scale can be applied, `-point-scale` can be used as the modifier. If no logical scale can be applied, use logical modifiers i.e. `-light`.
* Add a line break between different property group types.
* There are no standardized guidelines for mapping variables to other variables, but it is strongly encouraged that mappings are kept consistant and easy to reference.

    __Bad__
    ```css
    --blue: #005da8;
    --blue2: #00a0dd;
    --blue3: #acd5f8;
    --timing: .25s;
    --othertiming: 1s;
    ```

     __Good: Logicial Modifiers__
    ```css
    --color-blue: #005da8;
    --color-blue-light: #00a0dd;
    --color-blue-dark: #acd5f8;

    --timing-fast: .25s;
    --timing-slow: .1s;
    ```

     __Good: Point Scale__
    ```css
    --color-blue-10: #00a0dd;
    --color-blue-20: #005da8;
    --color-blue-30: #acd5f8;
    ```

**Nested Selectors**
* Following BEM or pseudo BEM should allow you to avoid nesting in most cases. This creates CSS that is both easier to maintain and smaller in size. When nesting does become needed, it should be kept as shallow as possible. A good code smell is to refactor and break out CSS that requires nesting beyond three levels deep.

**Breakpoints & Media Queries**
* __Write Desktop First CSS.__ [Reasoning].

    __Bad__

    ```css
    .column {
        display: block;
        width: 100%;
    }
    @media all and (min-width: 400px) {
        .column {
            display: table-cell;
            width: 50%;
        }
    }
    ```
    __Good__
    ```css
    .column {
        display: table-cell;
        width: 50%;
    }
    @media all and (max-width: 400px) {
        .column {
            display: block;
            width: 100%;
        }
    }
    ```
* __Don’t use device dimensions to determine breakpoints.__ The device landscape is always changing, so today’s values might be moot even just a year down the road. The device landscape is inherently fluid, so it’s our job to create designs that look and function beautifully on any screen instead of in just a few arbitrary buckets.

## Frameworks
### Middlemail

[Middlemail description]


### Skeletor

[IS THIS RELEVANT?]

Skeletor is a [Grunt](http://gruntjs.com)-powered, [Pattern Lab](http://patternlab.io)-centric, highly-customizable web project boilerplate and build tool created by the [DEG](http://www.degdigital.com) UI team. Skeletor uses [PostCSS](http://postcss.org) for CSS processing and [JSPM](http://jspm.io)/[SystemJS](https://github.com/systemjs/systemjs) for Javascript package management, module bundling/loading, and transpilation. Full Skeletor documentation is available [here](https://github.com/degdigital/skeletor).

### Pattern Lab

[IS THIS RELEVANT?]

Pattern Lab is a collection of tools to help you create atomic design systems. DEG uses Pattern Lab as a design & development tool, a prototyping & demo tool, and as an interactive style guide deliverable for clients. Although Pattern Lab comes with an out of the box partner starter kit, we have modified this kit to more closely resemble the types of projects we work on and practices we follow. Our modified version of Pattern Lab can be found within [Skeletor](https://github.com/degdigital/skeletor). Pattern Lab specific documentation can be found on the [Pattern Lab website](http://patternlab.io/).

## Design Patterns & Considerations

### Atomic Design
[IS THIS RELEVANT?]

The DEG UI team encourages the use of the [Atomic Design](http://bradfrost.com/blog/post/atomic-web-design) methodology for creating design systems. The basic gist of atomic design is to break interfaces down into fundamental building blocks and work up from there. Traditional atomic design consists of 5 distinct levels:
- __Atoms__: Basic building blocks. HTML tags, such as a form label, an input or a button.
- __Molecules__: Groups of atoms bonded together. Form label, input & button combined together.
- __Organisms__: Groups of molecules joined together to form a distinct section of an interface.
- __Templates__: Groups of organisms stitched together to form pages.
- __Pages__: Specific instances of templates.

DEG uses a modified version of these levels to simplify development, tie in better with design processes & deliverables, and to use terminology that is easier for clients to understand. Our version of atomic design consists of 4 dinstinct levels:
- __Basics__: Basic building blocks. Typography, colors, & basic HTML tags.
- __Components__: Groups of basics or other components combined together. Components should be nested into parent & child relationships when applicable.
- __Templates__: Groups of components combined together to create pages.
- __Pages__: Specific instances of templates.

### Email Client Support
[Email Client Support guidelines here]
https://docs.google.com/document/d/1D3vdUmuDUekxD_Lj5rpgvHiLQN_NVI7WuBwG338cq0A/edit

### Performance
[Email Based Performance guidelines and considerations here]

### Detailed Design Patterns & Anti-Patterns
Although projects do often present unique challenges, there are certain challenges we see repeated across many projects. Because of this, the DEG UI Email team maintains a set of client facing documentation on best practices for using and implementing common design patterns & anti-patterns including:
- [Email POVs Here]
- https://docs.google.com/document/d/1OlLqGrOzDMjBXpd7y6pVR4ChXyp3Z8GCn1PtzjoKiuQ/edit

## Tooling

### Editors
* Sublime Text

### CSS
* PostCSS
* Legacy Projects: Sass/Compass

### Task Runners
* Grunt
* Legacy Projects: Rake

### Visual Editors
* Photoshop
* Illustrator

### Virtual Machines
* VirtualBox

### ALM / Version Control
* JIRA
* Kanbanize
* Git

### Testing
* Litmus

