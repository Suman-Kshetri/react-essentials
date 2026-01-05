# Shadcn UI + Tailwind CSS Setup Guide (Vite + JavaScript)

Complete setup guide for configuring Shadcn UI and Tailwind CSS in a React.js project using Vite and JavaScript.

## Project Structure

```
my-project/
├── jsconfig.json
├── components.json
├── vite.config.js
├── package.json
├── src/
│   ├── index.css
│   ├── App.jsx
│   ├── lib/
│   │   └── utils.js
│   └── components/
│       └── ui/
```

---

## Resources To Setup From

- [Shadcn UI JavaScript Docs](https://ui.shadcn.com/docs/javascript)
- [Tailwind CSS with Vite](https://tailwindcss.com/docs/installation/using-vite)
- [Shadcn UI Components](https://ui.shadcn.com/docs/components)

---

## Step 1: Create Vite Project

```bash
npm create vite@latest my-project -- --template react
cd my-project
npm install
```

---

## Step 2: Install Tailwind CSS

### Install Tailwind CSS

Install `tailwindcss` and `@tailwindcss/vite` via npm.

```bash
npm install tailwindcss @tailwindcss/vite
```

### Import Tailwind CSS

Add an `@import` to your CSS file that imports Tailwind CSS.

**src/index.css**

```css
@import "tailwindcss";
```

---

## Step 3: Configure Vite & Path Aliases

### Configure `vite.config.js`

Add the `@tailwindcss/vite` plugin and configure path aliases.

**vite.config.js**

```js
import path from "path"
import react from "@vitejs/plugin-react"
import tailwindcss from '@tailwindcss/vite'
import { defineConfig } from "vite"

export default defineConfig({
  plugins: [react(), tailwindcss()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})
```

### Create `jsconfig.json`

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

---

## Step 4: Configure Shadcn UI

### Run the CLI

Run the `shadcn` init command to setup your project:

```bash
npx shadcn@latest init
```

This will:

- Create `components.json`
- Create `src/lib/utils.js`
- Configure your project for Shadcn UI components

---

## Step 5: Add Shadcn UI Components

Now you can add components using the Shadcn CLI:

```bash
npx shadcn@latest add button
npx shadcn@latest add card
npx shadcn@latest add input
```

Components will be added to `src/components/ui/`

---

## Step 6: Test Your Setup

### Update `src/App.jsx`

```jsx
import { Button } from "@/components/ui/button"

function App() {
  return (
    <div className="min-h-screen flex items-center justify-center">
      <div className="space-y-4">
        <h1 className="text-4xl font-bold">Shadcn UI + Tailwind CSS</h1>
        <Button>Click me</Button>
      </div>
    </div>
  )
}

export default App
```

### Run Development Server

```bash
npm run dev
```

---

## Common Commands

```bash
# Add a component
npx shadcn@latest add [component-name]

# Add multiple components
npx shadcn@latest add button card input

# List all available components
npx shadcn@latest add
```

---

## Troubleshooting

- If you get path alias errors, make sure `jsconfig.json` is in the root directory
- If Tailwind styles aren't working, verify `@import "tailwindcss";` is in your `src/index.css`
- Make sure `src/index.css` is imported in your `src/main.jsx`
