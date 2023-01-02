# Frontend Mentor - QR code component solution

This is a solution to the [QR code component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/qr-code-component-iux_sIO_H). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Useful resources](#useful-resources)
- [Author](#author)

## Overview

### Screenshot

![Screenshot](./screenshot.jpg)

### Links

- [Solution URL](https://www.frontendmentor.io/solutions/qr-code-component-0ok5JfXbJl)
- [Live Site URL](https://vyonizr.github.io/fm-qr-code-component/)

## My process

### Built with

- Plain HTML
- [Tailwind CSS](https://tailwindcss.com/)

### What I learned

In this challenge,I learned how to apply Tailwind CSS into a plain HTML project. First, use Tailwind CDN script for quicker development.

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
</body>
</html>
```

To serve the page, install [live-server](https://www.npmjs.com/package/live-server) globally and run this command:

```bash
live-server --host=localhost
```

But as stated by Tailwind's docs, we should not use CDN method for production. So After utilizing all the needed default classes, I initialized package manager.

```bash
yarn init
```

Install `tailwindcss`, `postcss-cli`, and `autoprefixer` as devDependencies.

```bash
yarn add tailwindcss postcss-cli autoprefixer -D
```

Create default Tailwind configuration file. This will create a file named `tailwind.js`.

```bash
npx tailwind init tailwind.js -full
```

Create a file named `postcss.config.js` and configured as shown below

```javascript
/* postcss.config.js */
const tailwindcss = require('tailwindcss');
module.exports = {
  plugins: [
    tailwindcss('./tailwind.js'),
    require('autoprefixer')
  ],
};
```

Create a file called `tailwind.css`

```css
/* tailwind.css */
@import "tailwindcss/base";
@import "tailwindcss/components";
@import "tailwindcss/utilities";
```

Run `postcss` script to generate `style.css`.

```bash
npx postcss tailwind.css -o style.css
```

By default, Tailwind will purge unused CSS classes. But, we have to define the `content` beforehand as its reference. In this case, we only have `index.html` thus the configuration written as:

```javascript
/* tailwind.js */
module.exports = {
  content: [
    './*.html',
  ],
  /* ... */
}
```

Then, insert `style.css` to `index.html` to replace Tailwind CDN

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="style.css"/>
  <!-- <script src="https://cdn.tailwindcss.com"></script> -->
</head>
<body>
</body>
</html>
```

For custom font required by the [style-guide.md](./style-guide.md), download Outfit font and put `Outfit-Bold.ttf` and `Outfit-Regular.ttf` on `public/fonts/outfit`. We only need this two because there are only two kinds of font weight needed: 400 (regular) and 700 (bold).

Configure `tailwind.css` again by adding these lines:

```css
@font-face {
  font-family: "Outfit";
  font-weight: 400;
  src: url("./public/fonts/outfit/Outfit-Regular.ttf");
}

@font-face {
  font-family: "Outfit";
  font-weight: 700;
  src: url("./public/fonts/outfit/Outfit-Bold.ttf");
}
```

In `tailwind.js`, add `Outfit` font in the first list of `sans` array so when you add `text-sans` class, it will be read properly.

```javascript
/* tailwind.js */
module.exports = {
  theme: {
    fontFamily: {
      sans: [
        'Outfit',
        /* ... */
      ]
    }
  }
}
```

To add colors from the requirement, add these lines in `tailwind.js`. We don't need to add white color as it is already provided by Tailwind itself.

```javascript
/* tailwind.js */
module.exports = {
  theme: {
    colors: ({ colors }) => ({
      /* ... */
      customLightGray: 'hsl(212, 45%, 89%)',
      customGrayishBlue: 'hsl(220, 15%, 55%)',
      customDarkBlue: 'hsl(218, 44%, 22%)'
    })
  }
}
```

For the usage, refere to [Color Customization](https://tailwindcss.com/docs/customizing-colors) section on Tailwind Docs.

To set custom font size required, in this case I name it `p` and then simply add class `text-p` to an element:

```javascript
/* tailwind.js */
module.exports = {
  theme: {
    fontSize:{
      /* ... */,
      p: ['15px', { lineHeight: '1.5rem' }],
    }
  }
}
```

Don't worry if your custom class does not work. It means it is not written on `style.css` yet. The solution is to re-run the build command.

```bash
npx postcss tailwind.css -o style.css
```

### Useful resources

- [How to add tailwindcss to a simple HTML Project](https://dev.to/raphaelmansuy/how-to-add-tailwindcss-to-a-simple-html-project-446g) - This helped me setting up Tailwind CSS for plain HTML project.

## Author

- Website - [vyonizr](https://vyonizr.com/)
- Frontend Mentor - [@vyonizr](https://www.frontendmentor.io/profile/vyonizr)
