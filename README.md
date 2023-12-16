**packages**

```
npm i -D eslint @typescript-eslint/parser eslint-config-prettier eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks lint-staged husky

npm i -D --save-exact prettier

npm i -D --legacy-peer-deps @typescript-eslint/eslint-plugin
```

```
Purposes:
- @typescript-eslint/parser: help eslint understand typescript
- eslint-config-prettier: prettier applied rules (put in extends)
- eslint-plugin-prettier: prettier rule sets (put in plugins)
- eslint-plugin-react: react apllied rules
- eslint-plugin-react-hooks: react hooks apllied rules
```

**.prettierrc**

```
{
  "printWidth": 80,
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true,
  "jsxSingleQuote": true,
  "bracketSpacing": true,
  "bracketSameLine": false,
  "arrowParens": "always",
  "trailingComma": "all"
}
```

**.eslintrc**

```
{
  "root": true,
  "env": { "browser": true, "es2022": true },
  "settings": {
    "react": { "version": "detect" }
  },
  "ignorePatterns": ["dist", ".eslintrc", "*.test.tsx"],
  "parser": "@typescript-eslint/parser", // language parser
  "plugins": ["prettier"], // set of rules, but not applied yet
  "extends": [ // preset applied rules
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react/recommended",
    "plugin:react/jsx-runtime",
    "plugin:react-hooks/recommended",
    "plugin:prettier/recommended"
  ],
  "parserOptions": { "sourceType": "module" },
  "rules": {
    "prettier/prettier": [1, { "endOfLine": "auto" }], // fix endline problem
    "react-hooks/rules-of-hooks": 2,
    "react-hooks/exhaustive-deps": 0,
    "react/jsx-no-useless-fragment": 1,
    "no-console": 1,
    "@typescript-eslint/no-unused-vars": 1,
    "@typescript-eslint/no-inferrable-types": 1,
    "@typescript-eslint/no-non-null-assertion": 0,
    "@typescript-eslint/no-explicit-any": 0
  },
  "overrides": [
    {
      "files": ["*.ts"],
      "rules": { "no-unused-vars": 0 } // ignore warning of unused variables in interface of typescript, @typescript-eslint/no-unused-vars already handle this
    }
  ]
}
```

**package.json**

```
  "lint": "eslint --ignore-path .eslintignore --max-warnings 0 \"./src/**/*.{js,jsx,ts,tsx}\"",
  "lint:fix": "eslint --ignore-path .eslintignore --fix \"./src/**/*.{js,jsx,ts,tsx}\"",
  "format": "prettier --ignore-path .gitignore --write \"./src/**/*.{js,jsx,ts,tsx,json,css,md}\"",
  "prepare": "husky install"
```

**.lintstagedrc**

```
{
  "*.{js,jsx,ts,tsx}": ["prettier -w", "eslint --max-warnings 0"],
  "*.{css,json,md}": ["prettier -w"]
}

```

**husky**

```
npx husky-init
npm i
npx husky set .husky/pre-commit "npx lint-staged"
```
