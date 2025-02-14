# Tested and working Clerk Auth Integration for Vite + React in cursor using Claude Sonnet 3.5(latest)

## Prompt:

Set up my clerk auth integration for our project using this attached step by step guide as well as an example project code repo that has been set up with a working nextjs project and clerk auth integration:

1. Install the Clerk React SDK

In your project’s root directory, install Clerk’s React SDK by running:

npm install @clerk/clerk-react

2. Configure Environment Variables
a. In Your Local Environment

    Create (or update) a file called .env.local in the root of your project.

    Add your Clerk Publishable Key. For example:

    VITE_CLERK_PUBLISHABLE_KEY=YOUR_PUBLISHABLE_KEY

    Replace YOUR_PUBLISHABLE_KEY with the actual key from your Clerk dashboard.

b. In Your Cloudflare Wrangler Configuration (if present)

    Open (or create) your wrangler.toml file.

    Under the [vars] section, add a placeholder for your Clerk key (and any other environment variables). For example:

    name = "your-app-name"
    type = "javascript"
    account_id = "your_account_id"
    workers_dev = true
    route = ""
    zone_id = ""

    [vars]
    VITE_CLERK_PUBLISHABLE_KEY = "pk_test_placeholder"
    EXAMPLE_API_TITLE = "example_key"

    Make sure that the key names match exactly (including the VITE_ prefix) so that both your local development and Cloudflare Pages environments have consistent configuration.

1. Update Your Application Code
a. Modify src/main.tsx

    Import Clerk Provider and Environment Variable:

    Edit src/main.tsx to import the ClerkProvider from @clerk/clerk-react and grab the publishable key from the environment. Ensure the app throws an error if the key is missing:

    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import App from './App';
    import './index.css';
    import { ClerkProvider } from '@clerk/clerk-react';

    // Get the Clerk Publishable Key from environment variables
    const PUBLISHABLE_KEY = import.meta.env.VITE_CLERK_PUBLISHABLE_KEY;

    if (!PUBLISHABLE_KEY) {
      throw new Error('Missing Clerk Publishable Key. Please add it to your .env.local file.');
    }

    ReactDOM.createRoot(document.getElementById('root')!).render(
      <React.StrictMode>
        <ClerkProvider publishableKey={PUBLISHABLE_KEY} afterSignOutUrl="/">
          <App />
        </ClerkProvider>
      </React.StrictMode>
    );

b. Update src/App.tsx to Use Clerk Components

    Integrate Clerk Components:

    Replace or update the content of src/App.tsx to include Clerk components for handling user authentication. For example:

import { SignedIn, SignedOut, SignInButton, UserButton } from '@clerk/clerk-react';

export default function App() {
  return (
    <header>
      <SignedOut>
        <SignInButton />
      </SignedOut>
      <SignedIn>
        <UserButton />
      </SignedIn>
    </header>
  );
}

This code uses:

    <SignedOut>: Renders its children (in this case, <SignInButton>) only when the user is signed out.
    <SignedIn>: Renders its children (here, <UserButton>) only when the user is signed in.


Clerk React Quickstart NextJS Example github repo:
<example>
Directory structure:
└── clerk-clerk-react-quickstart/
    ├── README.md
    ├── eslint.config.mjs
    ├── index.html
    ├── package.json
    ├── tsconfig.json
    ├── tsconfig.node.json
    ├── vite.config.ts
    ├── .env.sample
    ├── .prettierignore
    ├── .prettierrc
    ├── public/
    └── src/
        ├── App.tsx
        ├── index.css
        ├── main.tsx
        └── vite-env.d.ts


Files Content:

## Introduction

Clerk is a developer-first authentication and user management solution. It provides pre-built React components and hooks for sign-in, sign-up, user profile, and organization management. Clerk is designed to be easy to use and customize, and can be dropped into any React application.

After following the [Clerk React quickstart](https://clerk.com/docs/quickstarts/react), you will have learned how to:

- Create a new React application using Vite
- Install `@clerk/clerk-react`
- Set up your environment keys
- Import the Clerk Publishable Key
- Wrap your React app in `<ClerkProvider />`
- Use Clerk components to protect your content
- Embed the `<SignInButton />` and `<SignOutButton />`
- Deploy your application

### Branches of this repository

- `main`: The result of following the [Clerk React quickstart](https://clerk.com/docs/quickstarts/react).
- `integrate-react-router-dom-using-data-router`: The result of following the [Add React Router](https://clerk.com/docs/references/react/add-react-router#add-react-router-to-your-clerk-powered-react-application) guide.

## Deploy

Easily deploy the template to Vercel with the button below. You will need to set the required environment variables in the Vercel dashboard.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fclerk%2Fclerk-react-quickstart&env=VITE_CLERK_PUBLISHABLE_KEY,CLERK_SECRET_KEY&envDescription=Clerk%20API%20keys&envLink=https%3A%2F%2Fclerk.com%2Fdocs%2Fquickstart%2Freact&redirect-url=https%3A%2F%2Fclerk.com%2Fdocs%2Fquickstart%2Freact)

## Running the template

```bash
git clone https://github.com/clerk/clerk-react-quickstart
```

To run the example locally, you need to:

1. Sign up for a Clerk account at [https://clerk.com](https://dashboard.clerk.com/sign-up?utm_source=DevRel&utm_medium=docs&utm_campaign=templates&utm_content=10-24-2023&utm_term=clerk-react-quickstart).

2. Go to the [Clerk dashboard](https://dashboard.clerk.com?utm_source=DevRel&utm_medium=docs&utm_campaign=templates&utm_content=10-24-2023&utm_term=clerk-react-quickstart) and create an application.

3. Set the required Clerk environment variables as shown in [the example `env` file](./.env.sample).

4. `npm install` the required dependencies.

5. `npm run dev` to launch the development server.

## Learn more

To learn more about Clerk and React, check out the following resources:

- [Quickstart: Get started with React and Clerk](https://clerk.com/docs/quickstarts/react?utm_source=DevRel&utm_medium=docs&utm_campaign=templates&utm_content=10-24-2023&utm_term=clerk-react-quickstart)

- [Clerk Documentation](https://clerk.com/docs?utm_source=DevRel&utm_medium=docs&utm_campaign=templates&utm_content=10-24-2023&utm_term=clerk-react-quickstart)
- [Vite Documentation](https://vitejs.dev/guide/)

## Found an issue or want to leave feedback

Feel free to create a support thread on our [Discord](https://clerk.com/discord). Our support team will be happy to assist you in the `#support` channel.

## Connect with us

You can discuss ideas, ask questions, and meet others from the community in our [Discord](https://discord.com/invite/b5rXHjAg7A).

If you prefer, you can also find support through our [Twitter](https://twitter.com/ClerkDev), or you can [email](mailto:support@clerk.dev) us!

================================================
File: eslint.config.mjs
================================================
import globals from 'globals';
import pluginJs from '@eslint/js';
import tseslint from 'typescript-eslint';
import pluginReactConfig from 'eslint-plugin-react/configs/recommended.js';
import { fixupConfigRules } from '@eslint/compat';

export default [
  { files: ['**/*.{mjs,ts,jsx,tsx}'] },
  { languageOptions: { parserOptions: { ecmaFeatures: { jsx: true } } } },
  { languageOptions: { globals: globals.browser } },
  pluginJs.configs.recommended,
  ...tseslint.configs.recommended,
  ...fixupConfigRules(pluginReactConfig),
  {
    settings: {
      react: {
        version: 'detect',
        pragma: 'React',
        pragmaFrag: 'React.Fragment',
      },
    },
  },
  {
    rules: {
      'react/react-in-jsx-scope': 'off',
    },
  },
  {
    ignores: ['dist/'],
  },
];


================================================
File: index.html
================================================
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/clerk.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Clerk + React Quickstart</title>
  </head>

  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>


================================================
File: package.json
================================================
{
  "name": "clerk-react-quickstart",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "build": "tsc && vite build",
    "dev": "vite",
    "format": "prettier --write .",
    "lint": "eslint . --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
  "dependencies": {
    "@clerk/clerk-react": "^5.17.1",
    "react": "^18.3.1",
    "react-dom": "^18.3.1"
  },
  "devDependencies": {
    "@eslint/compat": "^1.2.3",
    "@eslint/js": "^9.15.0",
    "@types/react": "^18.3.12",
    "@types/react-dom": "^18.3.1",
    "@typescript-eslint/eslint-plugin": "^8.16.0",
    "@typescript-eslint/parser": "^8.16.0",
    "@vitejs/plugin-react": "^4.3.4",
    "eslint": "^9.15.0",
    "eslint-plugin-react": "^7.37.2",
    "eslint-plugin-react-hooks": "^5.0.0",
    "eslint-plugin-react-refresh": "^0.4.14",
    "globals": "^15.12.0",
    "prettier": "3.4.1",
    "typescript": "^5.7.2",
    "typescript-eslint": "^8.16.0",
    "vite": "^6.0.0"
  },
  "packageManager": "npm@10.9.0"
}


================================================
File: tsconfig.json
================================================
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}


================================================
File: tsconfig.node.json
================================================
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "ESNext",
    "moduleResolution": "bundler",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}


================================================
File: vite.config.ts
================================================
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
});


================================================
File: .env.sample
================================================
VITE_CLERK_PUBLISHABLE_KEY=pk_test_


================================================
File: .prettierignore
================================================
package-lock.json
node_modules
dist
README.md

================================================
File: .prettierrc
================================================
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80
}


================================================
File: src/App.tsx
================================================
import {
  SignInButton,
  SignedIn,
  SignedOut,
  UserButton,
} from '@clerk/clerk-react';

function App() {
  return (
    <header>
      <SignedOut>
        <SignInButton />
      </SignedOut>
      <SignedIn>
        <UserButton />
      </SignedIn>
    </header>
  );
}

export default App;


================================================
File: src/index.css
================================================
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

a {
  font-weight: 500;
  color: #646cff;
  text-decoration: inherit;
}
a:hover {
  color: #535bf2;
}

body {
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 320px;
  min-height: 100vh;
}

h1 {
  font-size: 3.2em;
  line-height: 1.1;
}

button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
}
button:hover {
  border-color: #646cff;
}
button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

@media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }
  a:hover {
    color: #747bff;
  }
  button {
    background-color: #f9f9f9;
  }
}


================================================
File: src/main.tsx
================================================
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App.tsx';
import './index.css';
import { ClerkProvider } from '@clerk/clerk-react';

const PUBLISHABLE_KEY = import.meta.env.VITE_CLERK_PUBLISHABLE_KEY;

if (!PUBLISHABLE_KEY) {
  throw new Error('Missing Publishable Key');
}

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <ClerkProvider publishableKey={PUBLISHABLE_KEY} afterSignOutUrl="/">
      <App />
    </ClerkProvider>
  </React.StrictMode>
);


================================================
File: src/vite-env.d.ts
================================================
/// <reference types="vite/client" />



</example>



