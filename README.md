# Capacitor Svelte App for ESC/POS printing

Demo app written in Svelte with TypeScript, using the [thermal-printer-cordova-plugin](https://github.com/paystory-de/thermal-printer-cordova-plugin) to print to a thermal printer.

## Development Notes

In my experience, the above-mentioned plugin does not play nice with vanilla JavaScript, with the module failing to import. Thus, I resorted to using the Svelte starter template, then running the TypeScript setup:

```
npx degit sveltejs/template svelte-typescript-app
cd svelte-typescript-app
node scripts/setupTypeScript.js
```

See [this blog post](https://svelte.dev/blog/svelte-and-typescript) for details setting up a Svelte TypeScript project using the Svelte template.

Another problem occured during build time, due to `@rollup/plugin-typescript`. The build will fail with the following error:

```
> svelte-app@1.0.0 build /Users/julianpatdu/Desktop/capacitor-svelte-ts-escpos
> rollup -c


src/main.ts → public/build/bundle.js...
[!] Error: Unexpected token (Note that you need plugins to import files that are not JavaScript)
node_modules/thermal-printer-cordova-plugin/src/definitions.ts (1:7)
1: export interface Printer {
          ^
2:     // Bluetooth
```

What fixed this was swapping `@rollup/plugin-typescript` for `rollup-plugin-typescript2`. See the `rollup.config.js` file of this project.