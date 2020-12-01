@jadetree/controls
==================

[Vue](https://vuejs.org/) controls for the Jade Tree budgeting software.

Install jadetree-currency using npm or yarn:

```shell
$ yarn install @jadetree/controls
```

You can then register Jade Tree Controls as a Vue plugin:

```javascript
import Vue from 'vue';
import { JtControls } from '@jadetree/controls';

Vue.use(JtControls);
```

This will automatically register the control components for use in Vue component
template files.  To use custom [Vue Formulate](https://vueformulate.com/) fields,
import the `JtFormulateLibrary` object and add it to the Vue Formulate plugin
initializer.

```typescript
import Vue from 'vue';
import { JtFormulateLibrary } from '@jadetree/controls';
import VueFormulate from 'vue-formulate';

// Setup Formulate with Jade Tree Customizations
Vue.use(VueFormulate, {
  classes: {
    outer: (
      context: { labelPosition: string | boolean },
      classes: string[],
    ) => (
      context.labelPosition === 'float'
        ? ['formulate-input--float']
        : classes
    ),
    element: (
      context: { labelPosition: string | boolean },
      classes: string[],
    ) => classes.concat([
      ...(context.labelPosition === 'float' ? ['formulate-float-label'] : []),
    ]),
  },
  library: {
    ...JtFormulateLibrary,
  },
  slotComponents: {
    label: 'JtFormulateLabel',
  },
});
```

Jade Tree Controls include [Tailwind CSS](https://tailwindcss.com/) themes by
default, and can be imported into your Vue application directly.  It is
recommended to skip PurgeCSS on the imported styles unless you point PurgeCSS
to the `@jadetree/controls` folder to find the style usages.

```css
/* In your application.css file */

/*! purgecss start ignore */
@import "@jadetree/controls/assets/tailwind/jt-controls.css";
/*! purgecss end ignore */
```

Included Components
-------------------

- Button
- Calendar (using [date-fns](https://date-fns.org))
- Currency Formulate Field (using [@jadetree/currency](https://github.com/asymworks/jadetree-currency))
- Check Box Formulate Field
- Date Picker Field
- Dialog
- Floating Label Formulate Fields
- Modal Controls
- Popup Controls
- Select and Combo Box
- Spinner

Installation
------------

Install Jade Tree Controls by running:

```shell
# Yarn
yarn add @jadetree/controls

# or, npm
npm install @jadetree/controls
```

Contribute
----------

- Issue Tracker: https://github.com/asymworks/jadetree-controls/issues
- Source Code: https://github.com/asymworks/jadetree-controls

API Documentation
-----------------

In Work

License
-------

The project is licensed under the BSD license.
