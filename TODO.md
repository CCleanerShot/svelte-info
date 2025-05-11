- look into `decode_character_references`'s behavior more closely (see if entities is actually more populated as the lifecycle of parsing goes, and if it continues with more files)


- find out if this is necessary: https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/read/script.js#L42:L43


- look into how comment nodes are generated


- test <textarea></textarea> during parsing step


- look into what void elements actually are in this


- look into https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/node_modules/.pnpm/zimmerframe@1.1.2/node_modules/zimmerframe/src/walk.js#L116-L119


- look into why svelte intellisense vscode extension doesn't work with the repo: https://github.com/CCleanerShot/svelte


- look into how svelte/actions work (it's just a typedef?)


- check if this prettier-ignore is removable now: https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/ambient.d.ts#L2-L3


- check if runes are actually functions (after finding out that runes remove function properties)


- look into if `$effect` attempting to catch the functionality of the function and not re-run. related code:
```
let test = $state(true)

// doesn't re-run
// $effect(() => {
//     console.log("cache")
//     setTimeout(() => {
//         test = !test;
//         console.log(test)
//     }, 1000)
// })

// re-runs
// $effect(() => {
//     console.log("cache", test)
//     setTimeout(() => {
//         test = !test;
//         console.log(test)
//     }, 1000)
// })
```