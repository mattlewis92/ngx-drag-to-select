# ngx-drag-to-select

[![travis](https://img.shields.io/travis/d3lm/ngx-drag-to-select/master.svg?label=Travis%20CI)](https://travis-ci.org/d3lm/ngx-drag-to-select)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![npm](https://img.shields.io/npm/v/ngx-drag-to-select.svg)](https://www.npmjs.com/package/ngx-drag-to-select)
[![npm License](https://img.shields.io/npm/l/ngx-drag-to-select.svg)](https://github.com/d3lm/ngx-drag-to-select/blob/master/LICENSE)

A lightweight, fast, configurable and reactive drag-to-select component for Angular 6 and beyond

## Demo

[Live Demo](https://d3lm.github.io/ngx-drag-to-select/)

## Playground

You can also fiddle with the library using [StackBlitz](https://stackblitz.com/edit/ngx-drag-to-select?file=app%2Fpages%2Fhome%2Fhome.component.html). Credits for the template go to [Bram Borggreve](https://twitter.com/beeman_nl).

## Features

- Drag to Select
- Shortcuts
- Customizable 💅
- Lightweight
- Easy to use
- Ready for AoT and SSR
- Complies with the [Angular Package Format](https://docs.google.com/document/d/1CZC2rcpxffTDfRDs6p1cfbmKNLA6x5O-NtkJglDaBVs/preview)
- Includes FESM2015, FESM5, and UMD bundles 📦
- It's fast 🏎
- Mobile friendly 📱
- Thoroughly tested 🚨

## Examples

- [Desktop Example](https://github.com/d3lm/ngx-drag-to-select/blob/master/src/app): Check out the `AppComponent`!
- [Mobile Example](https://github.com/d3lm/ngx-drag-to-select/blob/master/src/app/phone): There's a dedicated `PhoneComponent` component that uses all the tools and features from this library to implement a Google Inbox-like selection experience.

## Table of contents

- [Installation](#installation)
- [Setup](#setup)
- [Usage](#usage)
- [Configuration Options](#configuration-options)
- [API](#api)
- [FAQ](#faq)
- [Want to contribute?](#want-to-contribute)
- [For developers](#for-developers)
- [Versioning](#versioning)
- [Licence](#licence)

## Installation

```
npm install ngx-drag-to-select
```

or

```
yarn add ngx-drag-to-select
```

## Setup

Setting up `ngx-drag-to-select` is easy, and it only takes a few steps!

### Adding the CSS

The first step is to add the CSS and for that you have two options. Either you use the **default styles** or you can import the `ngx-drag-to-select` sass package directly. The latter gives you the option to override variables and customize for instance the look and feel of the selection rectangle.

**Using the default styles**

Copy `ngx-drag-to-select.css` to your project and add it as a `style` tag to your `index.html`.

If you are using sass you can import the css as follows:

```
@import "~ngx-drag-to-select/ngx-drag-to-select.css";
```

If you are using the [Angular CLI](https://github.com/angular/angular-cli) you can add it to your `angular.json`

```
"styles": [
  "styles.scss",
  "../node_modules/ngx-drag-to-select/ngx-drag-to-select.css"
]
```

**Using the sass package**

If you're using sass you can simply import the sass package. This allows you to [override the default variables](#overriding-sass-variables) to customize the library to your needs.

```
@import "~ngx-drag-to-select/scss/ngx-drag-to-select";
```

### Adding the module

In your `AppModule` import `DragToSelectModule` from `ngx-drag-to-select` and add it to the module imports:

```
import { DragToSelectModule } from 'ngx-drag-to-select';

@NgModule({
  imports: [
    DragToSelectModule.forRoot()
  ]
})
export class AppModule { }
```

That's it. You are now ready to use this library in your project. Make sure to call `forRoot()` only **once** in your `AppModule` and for feature modules you simply add the `DragToSelectModule` as is **without** calling `forRoot()`.

## Usage

Once you have installed the library and added the `DragToSelectModule` to your application you are ready to go.

Anywhere in your template add the `dts-select-container` component and wrap all items that you want to be selectable in this component.

Next, mark all selectable items with the `dtsSelectItem` directive. This connects each item with the container component.

Here's a complete example:

```
<dts-select-container #container="dts-select-container" [(selectedItems)]="selectedDocuments" (select)="someMethod($event)">
  <ul>
    <li [dtsSelectItem]="document" *ngFor="let document of documents">{{ document.name }}</li>
  </ul>
</dts-select-container>
```

## Configuration Options

This section gives you an overview of things you can customize and configure.

### Overriding sass variables

You can override the following variables:

| Variable                      | Type    | Default        | Description                                          |
| ----------------------------- | ------- | -------------- | ---------------------------------------------------- |
| `$dts-primary`                | Color   | `#7ddafc`      | Primary color                                        |
| `$select-box-color`           | Color   | `$dts-primary` | Color of the selection rectangle                     |
| `$select-box-removing-color`  | Color   | `$dts-primary` | Color of the selection rectangle when removing items |
| `$select-box-border-size`     | Unit    | `2px`          | Border size for the selection rectangle              |
| `$selected-item-border`       | Boolean | `true`         | Whether the selected item should get a border        |
| `$selected-item-border-color` | Color   | `#d2d2d2`      | Border color of the selected item                    |
| `$selected-item-border-size`  | Unit    | `1px`          | Border size of the selected item                     |
| `$box-shadow`                 | Boolean | `true`         | Whether the selected item should get a box shadow    |

If you wish to override one of these variables, make sure to do that **before** you import the sass package.

Example:

```
// Example for overriding the color of the selection retangle
$select-box-color: red;

@import "~ngx-drag-to-select/scss/ngx-drag-to-select";
```

Keep in mind that default styles are applied to all drag-to-select instances in your application. This means that if you override the color of the select box and set it so something like `red` then all instances render a `red` selection rectangle.

### Configuring `DragToSelectModule`

This library allows to you override certain options, such as

**`selectedClass`** (String)

Class that is added to an item when it's selected. The default class is `selected`. Note that if you override this option, you'll lose the default styling and must take care of this yourself.

**`shortcuts`** (Object)

`ngx-drag-to-select` supports a hand full of shortcuts to make our live easier when selecting items.

| Shortcut            | Default          | Description                                                                       |
| ------------------- | ---------------- | --------------------------------------------------------------------------------- |
| disableSelection    | `alt`            | Disable selection mode to allow selecting text on the screen within the drag area |
| toggleSingleItem    | `meta`           | Add or remove single item to / from selection                                     |
| addToSelection      | `shift`          | Add items to selection                                                            |
| removeFromSelection | `shift` + `meta` | Remove items from selection                                                       |

You can override these options by passing a configuration object to `forRoot()`.

Here's an example:

```
import { DragToSelectModule } from 'ngx-drag-to-select';

@NgModule({
  imports: [
    DragToSelectModule.forRoot({
      selectedClass: 'my-selected-item',
      shortcuts: {
        disableSelection: 'alt+meta'
      }
    })
  ]
})
export class AppModule { }
```

**Note**: If you override one of the shortscut you have to make sure they do not interfear with one another to ensure a smooth selecting experience.

#### Modifiers

When overriding the default shortcuts you can use the following modifier keys:

**`shift`**
**`alt`**
**`ctrl`**
**`meta`**

When using `meta`, it will be substituted with `ctrl` (for Windows) **and** `cmd` (for Mac). This allows for cross-platform shortcuts.

#### Shortcut alternatives

You can also define alternative shortcuts. For that, simply chain the shortcuts with a comma. Here's an example:

```
shortcuts: {
  disableSelection: 'alt+meta,shift+alt'
}
```

## API

`ngx-drag-to-select` comes with two main building blocks, a `dts-select-container` component and a `dtsSelectItem` directive.

### `dts-select-container`

**Inputs**

| Input              | Type       | Default | Description                                                                                                   |
| ------------------ | ---------- | ------- | ------------------------------------------------------------------------------------------------------------- |
| selectedItems      | Array<any> | /       | Collection of items that are currently selected                                                               |
| selectOnDrag       | Boolean    | `true`  | Whether items should be selected while dragging                                                               |
| disabled           | Boolean    | `false` | Disable selection                                                                                             |
| disableDrag        | Boolean    | `false` | Disable selection by dragging with the mouse. May be useful for mobile.                                       |
| selectMode         | Boolean    | `false` | If set to `true`, a _toggle_ mode is activated similar to the `toggleSingleItem` shortcut. Useful for mobile. |
| custom             | Boolean    | `false` | If set to `true`, all default styles for selected items will not be applied.                                  |
| selectWithShortcut | Boolean    | `false` | If set to `true`, items can only be selected when single clicking and applying a keyboard shortcut            |

Here's an example of all inputs in action:

```
<dts-select-container
  [(selectedItems)]="selectedDocuments"
  [selectOnDrag]="true"
  [disabled]="false"
  [disableDrag]="true"
  [selectMode]="true"
  [custom]="true"
  [selectWithShortcut]="false">
  ...
</dts-select-container>
```

- To get ahold of the selected items you can use a two-way data binding (`[()]`) aka _banana-in-the-box_ syntax. This means that whenever the selection changes, your property is updated accordingly. It will always reflect the current selection.

- Binding an expression to `selectOnDrag` will override the default value. When this option is set to `false`, it will **increase the performance** but you'll trade this for a slighly worse user experience.

**Outputs**

| Input            | Payload Type | Description                                                                                                                                        |
| ---------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| select           | Array<any>   | Event that is fired when the selection changes. The payload (`$event`) will be the list of selected items.                                         |
| itemSelected     | any          | Event that is fired when the item is selected. The payload (`$event`) will be the item's value                                                     |
| itemDeselected   | any          | Event that is fired when the item is deselected. The payload (`$event`) will be the item's value                                                   |
| selectionStarted | None         | Event that is fired when the user starts selecting items.                                                                                          |
| selectionEnded   | Array<any>   | Event that is fired when the user stops selecting items, typically by releasing the mouse button. The payload will be a list of all selected items |

Example:

```
<dts-select-container (select)="someMethod($event)" (itemSelected)="itemSelected($event)" (itemDeselected)="itemDeselected($event)">
  ...
</dts-select-container>
```

**Public Methods**

| Methods                                               | Description                                                 |
| ----------------------------------------------------- | ----------------------------------------------------------- |
| selectAll()                                           | Select all items within the drag area                       |
| clearSelection()                                      | Clear current selection                                     |
| update()                                              | Recalculate bounding box for the container and its children |
| <a href="#selectItems">selectItems(predicate)</a>     | Select all items `predicate` returns truthy for             |
| <a href="#deselectItems">deselectItems(predicate)</a> | Deselect all items `predicate` returns truthy for           |
| <a href="#toggleItems">toggleItems(predicate)</a>     | Toggle all items `predicate` returns truthy for             |

To access these methods on the container component you can either use the `@ViewChild()` decorator

```
import { Component, ViewChild } from '@angular/core';
import { SelectContainerComponent } from 'ngx-drag-to-select';

@Component({
  ...
})
export class AppComponent {
  @ViewChild(SelectContainerComponent) selectContainer: SelectContainerComponent;

  someMethod() {
    this.selectContainer.clearSelection();
  }
}
```

or use it within the template with a template reference variable

```
<button (click)="selectContainer.selectAll()">Select All</button>
<button (click)="selectContainer.clearSelection()">Clear Selection</button>

<dts-select-container #selectContainer="dts-select-container" [(selectedItems)]="selectedDocuments">
  ...
</dts-select-container>
```

> What if I want to use the `@ViewChild()` decorator but have multiple instances of the `dts-select-container` in my template?

In that case I would recommend to add template reference variables to your select containers and query them one by one using the variable name.

Here's an example:

```
<dts-select-container #documents>
  ...
</dts-select-container>

...

<dts-select-container #images>
  ...
</dts-select-container>
```

In the component you can then query them one by one:

```
import { Component, ViewChild } from '@angular/core';
import { SelectContainerComponent } from 'ngx-drag-to-select';

@Component({
  ...
})
export class AppComponent {
  @ViewChild('documents') documentContainer: SelectContainerComponent;
  @ViewChild('images') imagesContainer: SelectContainerComponent;

  someMethod() {
    this.documentContainer.clearSelection();
  }

  someOtherMethod() {
    this.imagesContainer.selectAll();
  }
}
```

**Select Box**

Each instance of the `dts-select-container` renders its own select box. Based on the current selection mode, either adding or removing, the container
adds corresponding css classes for more flexibility in styling. For adding items to the current selection, either in normal or extended mode, the select box gets a class of `dts-adding`. For removing items the class will be `dts-removing`. Both classes can be used to override the look and feel based on the selectio mode.

For instance, the color of the select box, when removing items, can be styled with a separate variable `$select-box-removing-color`. If the color should be the same for both adding and removing, the `$dts-primary` variable can be used.

#### <a id="selectItems"></a> `selectItems(predicate)`

Iterates over collection of `SelectItemDirective`'s, selecting all items from that collection that meet the condition specified in the `predicate` function. The `predicate` is invoked with one argument `item`, which is equivalent to the value returned by `SelectItemDirective.value`.

**Arguments**

`predicate ((item: T) => boolean)`: The function invoked per iteration.

**Example**

```
import { Component, ViewChild } from '@angular/core';
import { SelectContainerComponent } from 'ngx-drag-to-select';

@Component({
  ...
})
export class AppComponent {
  @ViewChild(SelectContainerComponent) selectContainer: SelectContainerComponent;

  someMethod() {
    this.selectContainer.selectItems(item => item.id === 1)
  }
}
```

#### <a id="deselectItems"></a> `deselectItems(predicate)`

Iterates over collection of `SelectItemDirective`'s, deselecting all items from that collection that meet the condition specified in the `predicate` function. The `predicate` is invoked with one argument `item`, which is equivalent to the value returned by `SelectItemDirective.value`.

**Arguments**

`predicate ((item: T) => boolean)`: The function invoked per iteration.

**Example**

```
import { Component, ViewChild } from '@angular/core';
import { SelectContainerComponent } from 'ngx-drag-to-select';

@Component({
  ...
})
export class AppComponent {
  @ViewChild(SelectContainerComponent) selectContainer: SelectContainerComponent;

  someMethod() {
    this.selectContainer.deselectItems(item => item.id === 1)
  }
}
```

#### <a id="toggleItems"></a> `toggleItems(predicate)`

Iterates over collection of `SelectItemDirective`'s, toggling all items from that collection that meet the condition specified in the `predicate` function. The `predicate` is invoked with one argument `item`, which is equivalent to the value returned by `SelectItemDirective.value`.

**Arguments**

`predicate ((item: T) => boolean)`: The function invoked per iteration.

**Example**

```
import { Component, ViewChild } from '@angular/core';
import { SelectContainerComponent } from 'ngx-drag-to-select';

@Component({
  ...
})
export class AppComponent {
  @ViewChild(SelectContainerComponent) selectContainer: SelectContainerComponent;

  someMethod() {
    this.selectContainer.toggleItems(item => [1, 2, 3].includes(item.id))
  }
}
```

### `dtsSelectItem`

The `dtsSelectItem` directive is used to mark DOM elements as selectable items. It takes an input to control the value that is used when the item was selected. If the input is not specified, it will use the directive instance as a default value.

**Inputs**

| Input         | Type | Default            | Description                                  |
| ------------- | ---- | ------------------ | -------------------------------------------- |
| dtsSelectItem | any  | Directive Instance | Value that is used when the item is selected |

Example:

```
<dts-select-container>
  <ul>
    <li [dtsSelectItem]="document" *ngFor="let document of documents">{{ document.name }}</li>
  </ul>
</dts-select-container>
```

**Public Properties**

| Methods  | Type    | Description                         |
| -------- | ------- | ----------------------------------- |
| selected | Boolean | Whether the item is selected or not |

You can access this property in a similar why you access methods on the `dts-select-container` component using either a template reference variable or programmatically with the `@ViewChild()` decorator.

Example:

```
<dts-select-container>
  <ul>
    <li [dtsSelectItem]="document" #item *ngFor="let document of documents">
      {{ document.name }}
      <i class="fa fa-check" *ngIf="item.selected"></i>
    </li>
  </ul>
</dts-select-container>
```

## FAQ

### Is this library AoT and Universal compatible?

Yes.

### Does this library work with Angular 5.x?

The latest version that supports Angular 5.x is 1.1.1. You can still install it via npm or yarn, e.g. `npm install ngx-drag-to-select@1.1.1`.

Note, that we try to always keep up with Angular's latest version, hence, older versions will not receive bug fixes nor new features.

### Does this library work with mobile?

Yes. This library provides features that you need to implement a mobile version. Check out the [Mobile Example](https://github.com/d3lm/ngx-drag-to-select/blob/master/src/app/phone), specifically the `PhoneComponent` component that uses all the tools and features from this library to implement a Google Inbox-like selection experience.

### How do I deal with nested scrollable containers?

Suppose, we have the following markup:

```html
<body>
  ...
  <div class="scrollable"><dts-select-container #container="dts-select-container"> ... </dts-select-container></div>
</body>
```

Here we have another wrapper elements that wraps the `dts-select-container`. This element is **scrollable**. The library does not account for any scrollable elements but the `dts-select-container` itself as well as the body. If you have other nested scrollable containers, and the rendering of the select-box seems to be off, you have to listen for the `scroll` event on your scrollable element and call `update` on the `dts-select-container`. This will make sure that whenever you scroll, the position of the select-container and its items on the screen are re-calculated.

Check out the solution to the problem:

```html
<body>
  ...
  <div class="scrollable" (scroll)="container.update()">
    <dts-select-container #container="dts-select-container"> ... </dts-select-container>
  </div>
</body>
```

Here we listen for `scroll` on the `div` and call `container.update()` in case the event is fired.

In order not to kill the performance, because the `scroll` event is called many many times, you may want to **throttle** it to only call `update` every 16ms or so.

## Want to contribute?

If you want to file a bug, contribute some code, or improve our documentation, read up on our [contributing guidelines](CONTRIBUTING.md) and [code of conduct](CODE_OF_CONDUCT.md), and check out [open issues](/issues).

## For developers

If you want to set up `ngx-drag-to-select` on your machine for development, head over to our [developers guide](DEVELOPERS_GUIDE.md) and follow the described instructions.

## Versioning

`ngx-drag-to-select` will be maintained under the Semantic Versioning guidelines. Releases are numbered with the following format:

```
<MAJOR>.<MINOR>.<PATCH>
```

1.  **MAJOR** versions indicate incompatible API changes,
2.  **MINOR** versions add functionality in a backwards-compatible manner, and
3.  **PATCH** versions introduce backwards-compatible bug fixes.

For more information on SemVer, please visit [http://semver.org](http://semver.org).

## Licence

MIT © [Dominic Elm](http://github.com/d3lm)
