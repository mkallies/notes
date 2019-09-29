# TypeScript

- [Introduction to TypeScript](https://www.swyx.io/talks/intro-to-typescript)
- [TypeScript cheatsheet - react](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet)
- [TypeScript cheatsheet - react+redux](https://github.com/piotrwitek/react-redux-typescript-guide)
- [TypeScript cheatsheet](https://github.com/rmolinamir/typescript-cheatsheet)

## Do not do

- Functional changes at the same time

- Be perfect

- Forget to add tests for types

## Converting to TS

### 1

- Rename .js to .ts or .tsx

- Allow implicit any

- Fix things

### 2

- add noImplicitAny: true

- use explicit any if needed

- add types from @types

### 3

- Slowly remove explicit anys and enable strict mode

- strictNullChecks

- strict

- strictFunctionTypes

- strictBindCallApply

- Do this in small chunks

- Try to avoid unsafe casts

## Generics

- When to use

- Type parameters

- Constraints
