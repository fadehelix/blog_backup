title: 'Lintowanie React Native '
author: Adam Dziendziel
tags:
  - ReactNative
categories: []
date: 2017-06-02 10:17:00
---
## Co to jest linter i dlaczego go używać?

## Popularne lintery

* XO
* ESlint
* CSSlint
* SASSlint ?

## Zaprośmy ESlint do tańca
https://medium.com/the-react-native-log/getting-eslint-right-in-react-native-bd27524cc77b < zweryfikować czy to prawda

`./node_modules/.bin/eslint --init` i odpowiadamy na pytania:

```
? How would you like to configure ESLint? Answer questions about your style
? Are you using ECMAScript 6 features? Yes
? Are you using ES6 modules? Yes
? Where will your code run? Browser
? Do you use CommonJS? Yes
? Do you use JSX? Yes
? Do you use React? Yes
? What style of indentation do you use? Spaces
? What quotes do you use for strings? Single
? What line endings do you use? Unix
? Do you require semicolons? Yes
? What format do you want your config file to be in? JSON
```

### Własne reguły
__Cztery spacje na dwie__