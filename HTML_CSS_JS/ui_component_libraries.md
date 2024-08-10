<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

# Ui Component Libraries

<!-- TOC -->

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