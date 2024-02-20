[Home](./README.md)

# Ui Component Libraries

## Table of Contents
<!-- TOC -->

- [Ui Component Libraries](#ui-component-libraries)
	- [Table of Contents](#table-of-contents)
	- [Shadcn UI](#shadcn-ui)
		- [Installation with Solid JS](#installation-with-solid-js)
	- [Material UIMUI](#material-uimui)

<!-- /TOC -->

## Shadcn UI

### Installation with Solid JS
1. Add tailwind css
1. Install `npm install tailwindcss-animate class-variance-authority clsx tailwind-merge`
1. Update tsconfig.json
```
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```
1. Update vite.config.ts
```
import { defineConfig } from 'vite'
import solid from 'vite-plugin-solid'
import path from 'path'

export default defineConfig({
  plugins: [solid()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})
```
1. Run `npm install shadcn-solid`
1. Run `npx shadcn-solid@latest init`
1. Install your components

## Material UI(MUI)