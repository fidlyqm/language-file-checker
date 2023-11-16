# language-file-checker
- Objective: to detect discrepencies between different language files

## Installation
- `git clone https://github.com/fidlyqm/language-file-checker.git`
- `npm install`
- `npm run dev`
- see `http://localhost:5173/`

### How to use ?
- `en.js`(English) will be the main language file.
- paste in the latest language file (`en.js`, `ms.js`, `zh.js`), for example `src/lang/en.js`

## Remark
- the logic only expects single nested property, for example:
```
  route: {
    Reject:"Reject",
    GAETerminationView:"GAE Termination View",
    GAETermination: "GAE Termination",
    GoldStorageAccountView: "Gold Storage Account - View",
  }
```
- so, `route.Reject` is readaable, but `route.Reject.xxxx` will not be readable