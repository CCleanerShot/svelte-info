- look into `decode_character_references`'s behavior more closely (see if entities is actually more populated as the lifecycle of parsing goes, and if it continues with more files)

- find out if this is necessary: https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/read/script.js#L42:L43

- look into how comment nodes are generated

- test <textarea></textarea> during parsing step

- look into what void elements actually are in this

- look into https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/node_modules/.pnpm/zimmerframe@1.1.2/node_modules/zimmerframe/src/walk.js#L116-L119

- look into why svelte intellisense vscode extension doesn't work with the repo: https://github.com/CCleanerShot/svelte

- look into how svelte/actions work (it's just a typedef?)