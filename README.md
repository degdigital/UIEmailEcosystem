# UI Email Ecosystem
*DEG UI Email Code Standards, Design Patterns, Frameworks & Tooling*

## Table of Contents
  1. [Code Style Guide](#code-style-guide)
    - [HTML](#html)
    - [CSS Inline Styles](#css-inline-styles)
    - [CSS Stylesheets](#css-stylesheets)
  2. [Frameworks](#frameworks)
    - [Middlemail](#middlemail)
    - [Project Hubs](#project-hubs)
  3. [Design Patterns & Considerations](#design-patterns--considerations)
    - [Modular Design](#modular-design)
    - [Detailed Design Patterns & Anti-Patterns](#detailed-design-patterns--anti-patterns)
    - [Email Client Support](#email-client-support)
  4. [Tooling](#tooling)
    - [Editors](#editors)
    - [CSS](#css-1)
    - [Task Runners](#task-runners)
    - [Visual Editors](#visual-editors)
    - [ALM/Version Control](#alm)
    - [Testing](#testing)

## Code Style Guide

### HTML
**Formatting & Syntax**
* Use tabs (4 spaces) for indentation
* Nested elements should be indented once
* Don’t omit optional closing tags (e.g. `</tr>`, `</td>`, or `</body>`).

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

**HTML5 doctype**
* HTML5 (HTML syntax) is preferred for all HTML documents.
* Enforce standards mode where possible for more consistent rendering with this simple doctype at the beginning of every HTML page: `<!DOCTYPE html>`.

**Hybrid Layouts**
[HYBRID LAYOUT STANDARDS HERE]

### CSS Inline Styles
When building emails, all baseline styles should be included inline to achieve appropriate rendering across email clients.

[INLINE STYLE STANDARDS & GUIDELINES]

[AVOID DOING THESE THINGS WHEN WRITING INLINE STYLES]

### CSS Stylesheets
CSS Stylesheets are utilized when an email is built in the traditional responsive manner or as progressive enhancement when needed.

**Sass**
* DEG utilizes [Sass](http://sass-lang.com/) to process CSS files and aims to write modern and future-friendly CSS based on W3C specifications while avoiding the proprietary syntax of preproccesors whenever possible.

* [Middlemail](https://github.com/degdigital/middlemail/) comes preconfigured with Sass, and will output the compiled CSS into a `<style>` tag in the `<head>` of the HTML file on build, but developers are encouraged to adjust this behavior as the need arises on a per-project basis.

**Organization**
* CSS should be organized into logical partials and follow DEG's modified Atomic Email CSS structure of Basics, Components, Templates & Utilities. These partials will be processed using Sass and the available configuration options in Middlemail.

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
* Use ID selectors sparingly, if at all
* Use classes over generic element tags when possible
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

**Nested Selectors**
* When nesting is needed, it should be kept as shallow as possible. A good code smell is to refactor and break out CSS that requires nesting beyond three levels deep.

**Breakpoints & Media Queries**
* __Write Desktop First CSS.__ Due to the inherent nature of email development and support, desktop first media queries should be utilized.
 __Don’t use device dimensions to determine breakpoints.__ The device landscape is always changing, so today’s values might be moot even just a year down the road. Email is inherently fluid, so it’s our job to develop emails that look and function beautifully on any screen instead of in just a few arbitrary buckets.

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

## Frameworks
### Middlemail
[MiddleMail](http://degdigital.github.io/MiddleMail/) is a responsive email framework built with DEG's modern email workflow in mind. Middlemail is built on top of the Ruby based [Middleman](https://middlemanapp.com/) static site generator and features:
* Modular Components
* Integrated Sass
* JSON/Yaml Data
* Grunt tasks for automated build processes
* Project Hubs

### Project Hubs
DEG utilizes the concept of [Project Hubs](https://24ways.org/2013/project-hubs/) as a design & development tool, a prototyping & demo tool, and as an interactive template toolkit deliverable for clients. A basic Project Hub setup is included with Middlemail which you're encouraged to customize based on your specific project needs.

## Design Patterns & Considerations

### Modular Design
The DEG UI Email team encourages the use of modular design for creating design systems and template toolkits. The basic gist of modular design is to break components down into fundamental building blocks that can be duplicated, deleted, or reordered as neccesary on a per send basis.

### Hybrid, Responsive or Fluid?
The DEG UI Email team has a variety of techniques that can be utilized when designing and developing an email. However, because each technique has advantages and disadvantages, we do not default to a single one for every project. Because [every case is different](http://labs.actionrocket.co/hybrid-is-the-answer-is-it-the-right-question) we work to define the approach most suitable to a given projects specific needs.

### Interactive Email
DEG fully imbraces the emergence of interactive email. However, we discourage it's use as solely a new & flashy tactic that only email designers and developers will notice or care about. When utlizing interactive techniques, it's vital that a use case is defined that either works to reduce friction or provide a greater user experience than could be achieved without interactivity.

### Detailed Design Patterns & Anti-Patterns
Although projects do often present unique challenges, there are certain challenges we see repeated across many projects. Because of this, we maintain the [DEG Email Design Guide](https://docs.google.com/document/d/1OlLqGrOzDMjBXpd7y6pVR4ChXyp3Z8GCn1PtzjoKiuQ/edit) as a set of client facing documentation on best practices for using and implementing common design patterns & anti-patterns.

### Email Client Support
DEG uses the concept of Graded Email Client Support, which defines the current set of email clients that should receive a verified, usable experience. However, trying to deliver the same "A-grade" experience across all tested email clients isn't cost effective and forces you to design and develop for the lowest common denominator. We support a tiered approach to design, development, and testing that will allow us to deliver the best experience possible to each individual user. We encourage each project to define their own tiers that serve their users and stakeholders best.

For a more detailed explanation and a guide to help determine what email clients to support, view our [Email Client Support Guide](https://docs.google.com/document/d/1D3vdUmuDUekxD_Lj5rpgvHiLQN_NVI7WuBwG338cq0A/edit) on Google Docs.

## Tooling

### Editors
* Sublime Text

### CSS
* Sass

### Task Runners
* Grunt
* Legacy Projects: Rake

### Visual Editors
* Photoshop
* Illustrator

### ALM / Version Control
* JIRA
* Kanbanize
* Git

### Testing
* Litmus

