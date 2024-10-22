
# Template Svelte 5 with Flowbite Svelte

This guide helps you set up a Svelte 5 project with **Flowbite Svelte** for UI components, **Tailwind CSS**, and **Flowbite Icons**. Follow the steps below to scaffold your project and get started!

## Prerequisites

Make sure you have the following installed:
- [Node.js](https://nodejs.org/)
- [pnpm](https://pnpm.io/installation) (or another package manager like npm or yarn)

---

## Project Setup

### 1. Create the Svelte Project

Use the Svelte CLI to create a new SvelteKit project.

```bash
npx sv create svelte@latest svelte-5-flowbite-template
```

During project creation, you’ll be prompted with several options. Follow the responses outlined below:

```bash
┌ Welcome to the Svelte CLI! (v0.5.7)
│
◇ Which template would you like?
│ SvelteKit minimal
│
◇ Add type checking with Typescript?
│ Yes, using Typescript syntax
│
◆ Project created
│
◇ What would you like to add to your project?
│ tailwindcss
│
◇ Which plugins would you like to add?
│ typography, forms, container-queries, aspect-ratio
│
◇ Which package manager do you want to install dependencies with?
│ pnpm
│
◆ Successfully setup integrations
│
◇ Successfully installed dependencies
│
◇ Project next steps ─────────────────────────────────────────────────────╮
│                                                                          │
│  1: cd svelte-5-flowbite-template                                        │
│  2: git init && git add -A && git commit -m "Initial commit" (optional)  │
│  3: pnpm run dev -- --open                                               │
│                                                                          │
│  To close the dev server, hit Ctrl-C                                     │
│                                                                          │
│  Stuck? Visit us at https://svelte.dev/chat                              │
│                                                                          │
├──────────────────────────────────────────────────────────────────────────╯
└ You're all set!
```

### 2. Navigate to the Project Folder

Once your project is created, move into the newly created directory:

```bash
cd svelte-5-flowbite-template
```

### 3. Initialize a Git Repository

To initialize version control for your project, run the following commands:

```bash
git init
git add -A
git commit -m "Initial commit"
```

### 4. Install Tailwind (Optional)

If you didn’t choose Tailwind CSS during the initial setup, you can add it later with the following command:

```bash
npx svelte-add@latest tailwindcss
```

### 5. Install Flowbite Svelte

Install **Flowbite Svelte** and its dependencies:

```bash
pnpm i -D flowbite-svelte flowbite
```

### 6. Install Flowbite Icons (Optional)

Add **Flowbite Icons** to your project:

```bash
pnpm i -D flowbite-svelte-icons
```

### 6. Install Flowbite Blocks (Optional)

Add **Flowbite Blocks** to your project:

```bash
pnpm i -D flowbite-svelte-blocks
```


### 7. Update Tailwind Configuration

Update the `tailwind.config.cjs` file in your project’s root directory to include Flowbite’s configurations:

```js
import flowbitePlugin from 'flowbite/plugin'

import type { Config } from 'tailwindcss';

export default {
    content: ['./src/**/*.{html,js,svelte,ts}', './node_modules/flowbite-svelte/**/*.{html,js,svelte,ts}'],
    darkMode: 'selector',
    theme: {
        extend: {
            colors: {
                // flowbite-svelte
                primary: {
                    50: '#FFF5F2',
                    100: '#FFF1EE',
                    200: '#FFE4DE',
                    300: '#FFD5CC',
                    400: '#FFBCAD',
                    500: '#FE795D',
                    600: '#EF562F',
                    700: '#EB4F27',
                    800: '#CC4522',
                    900: '#A5371B'
                }
            }
        }
    },
    plugins: [flowbitePlugin]
} as Config;
```

---

Now you are ready to start building your Svelte project with Flowbite Svelte and Tailwind CSS! Happy coding!
