# How to set up a project with Vue.js and Tailwind CSS

This assumes you have the Vue CLI installed.

## Set up the Vue project

```shell
vue create myproject
```

## Adding Tailwind

### Install

Install Tailwind and its dependencies

```shell
npm install -D tailwindcss@npm:@tailwindcss/postcss7-compat @tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

### Create config files

Generate a `tailwind.config.js` file and `postcss.config.js` file

```shell
npx tailwindcss init -p
```

Next, configure Tailwind to purge unused styles in production. The `purge: []` attribute in `tailwind.config.js` should be changed to `purge: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}']`

Now your `tailwind.config.js` should look like this:

```
// tailwind.config.js
module.exports = {
    purge: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
    darkMode: false, // or 'media' or 'class'
    theme: {
        extend: {},
    },
    variants: {
        extend: {},
    },
    plugins: [],
}
```

### Include Tailwind in your CSS

Create a file in the `./src/assets/css` directory (if this directory does not exist, create it) called `tailwind.css` and add the following

```
/*! @import */
@import "tailwindcss/base";
@import "tailwindcss/components";
@import "tailwindcss/utilities";
```

Finally, import `tailwind.css` in your `./src/main.js` file

```
import "./assets/css/tailwind.css";
```

# Customizing Tailwind

## Changing breaksizes from min width to max width

In your `tailwind.config.js` file, add a `screens` section to the `theme` section in `module.exports`

```
module.exports = {
  theme: {
    screens: {
      '2xl': {'max': '1535px'},
      // => @media (max-width: 1535px) { ... }

      'xl': {'max': '1279px'},
      // => @media (max-width: 1279px) { ... }

      'lg': {'max': '1023px'},
      // => @media (max-width: 1023px) { ... }

      'md': {'max': '767px'},
      // => @media (max-width: 767px) { ... }

      'sm': {'max': '639px'},
      // => @media (max-width: 639px) { ... }
    }
  }
}
```

<sub>Note: Do not delete everything else in `module.exports` as this example shows. Simply add the `screens` section and leave everything else untouched</sub>

Now breakpoints will work for desktop development in mind first.

In other words, adding a `flex` class will add the class for every screen, and adding `md:flex-col` will change the flex direction to columns for _medium screens or smaller_, rather than the other way around (`flex-col` being active for meduim screens or larger).

[Tailwind: Customizing the default breakpoints for your project.](https://tailwindcss.com/docs/breakpoints)

## Adding Google fonts

### Find a font

Once you've found a font you like, make note of the `@import` and `font-family:` parts given by Google Fonts. For example, for **Quicksand**:

```
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@500&display=swap');
font-family: 'Quicksand', sans-serif;
```

### Add configuration

Next, go to your `tailwind.config.js` file and add the `fontFamily` section to the `theme` section in `module.exports`

In there, add a class name as a key (this can be anything you like), with and array of strings as a value. The array contains each `font-family:` attribute given by Google Fonts, in order:

```
module.exports = {
  theme: {
    fontFamily: {
      'quicksand': ['Quicksand', 'sans-serif']
    }
  }
}
```

<sub>Note: Again, do not delete everything else in `module.exports` as this example shows. Simply add the `fontFamily` section and leave everything else untouched</sub>

### Import font

Finally, in your `./src/assets/css` directory (or whatever directory your `tailwind.css` file is in), add a `fonts.css` file if it doesn't already exist.

In there, add your `@import`:

```
/* Quicksand (500), sans-serif */
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@500&display=swap');
```

Go to `./src/main.js` and import your `fonts.css` file if it is not already imported.

```
import "./assets/css/fonts.css";
```

Now just add the `font-quicksand` class (or whatever class name you gave your font) to an element in your webpage to change the font!

[Tailwind: Utilities for controlling the font family of an element.](https://tailwindcss.com/docs/font-family)