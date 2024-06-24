This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.

## My instructions

Cd to empty project folder and run `npx create-next-app@latest .`
Choose all options as Yes, except last aliases as No

PRETTIER
Install `npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier`

HUSKY and LINT
Install `npm install --save-dev husky lint-staged`

UPDATE eslintrc.json to include prettier

```
{
  "extends": ["eslint:recommended", "next", "next/core-web-vitals", "prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error"
  }
}
```

Create `.prettierrc` and (optionally) `.prettierignore` files

- .prettierignore

```
# Ignore artifacts:
.next/

# Ignore specific files:
package-lock.json
```

- .prettierrc (basic standard settings, google, generate with ChatGPT for more)

```
{
  "semi": true,
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2,
  "useTabs": false,
  "trailingComma": "es5",
  "bracketSpacing": true
}
```

Replace "lint" in `package.json` with the below

```
"lint": "eslint src --ext ts,tsx,js,jsx --report-unused-disable-directives --max-warnings 0",
```

Add additional below to `package.json` scripts

```
"lint:fix": "eslint src --ext js,jsx,ts,tsx --fix",
 "format": "prettier --write 'src/**/*.{js,jsx,ts,tsx,css,html}'"
```

Add additional below to `package.json` root

```
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm run lint && npm run format"
    }
  },
  "lint-staged": {
    "src/**/*.{js,jsx,ts,tsx,css,html}": [
      "npm run lint",
      "npm run format"
    ]
  }
```

Create `.husky` file with the command `npx husky init`
Add `npx lint-staged` line to `.husky/pre-commit` file

Add to package.json
`npm install --save-dev @commitlint/{cli,config-conventional}`

Add into `.husky/commit-msg` the below

```
npx --no-install commitlint --edit "$1"
```

Commit your changes, if errors run `npm run lint:fix`
