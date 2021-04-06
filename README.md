# tailwind-vscode

Are you authoring VS Code extensions with webviews? Step right up! This is a plugin for Tailwind that exposes VS Code's theme colors as Tailwind colors — with all of the variants (`bg`, `text`, `border`, etc…) Now you can author styles for your extension's webviews with Tailwind and use the active VS Code theme colors.

No, this is not a plugin for VS Code! Your absolutely should check out the [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) plugin, though. Not gonna lie, it's pretty fantastic.

## How do I use it?

Add via your favorite package manager. 

```bash
$ npm i -D tailwind-vscode
$ # or yarn, I ain't gonna judge
$ yarn add -D tailwind-vscode
```

Then add the plugin to your `tailwind.config.js`:

```js
module.exports = {
  /* other config stuff here */
  plugins: [require('tailwind-vscode')],
}
```

And style components!

```jsx
<input className='bg-vscode-input-background text-vscode-input-foreground border-vscode-input-border focus:border-vscode-inputOption-activeBorder'/>
```

Doing a little celebratory dance in your chair is optional but encouraged.

The [VS Code theme colors](https://code.visualstudio.com/api/references/theme-color) are represented as Tailwind colors under `vscode`, with hyphens subtituted for periods (`foo.bar` → `foo-bar`).

## How does it work?

Webviews are exposed inside an `<iframe>`. If you open the webview's developer tools and inspect the `<html>`, you'll see a style property with a honking large list of [CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties), also known by their rapper name, "variables".

These are injected by VS Code, and contain the style colors defined by the active VS Code theme. When a user changes the theme, the variables change. Voilà, themeability inside webviews.

Only, once you get used to Tailwind-y everything, using those color variables is quite jarring.

This plugin creates a `vscode` Tailwind [color object](https://tailwindcss.com/docs/customizing-colors#color-object-syntax) with definitions for every [VS Code theme color](https://code.visualstudio.com/api/references/theme-color). 

You could map these variables manually, like so:

```js
module.exports = {
  theme: {
    extend: {
      colors: {
        vscode: {
          'contrastBorder': 'var(--vscode-contrastBorder)',
          'focusBorder': 'var(--vscode-focusBorder)',
          'foreground': 'var(--vscode-foreground)',
          'widget-shadow': 'var(--vscode-widget-shadow)'
          /* … and 500 more */
```

But this is tedious. Use this plugin and spend your time on loftier pursuits.

## License

MIT



