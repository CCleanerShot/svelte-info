- ONLY MATCHES TS
svelte compiler's regex for checking the lang attribute only checks if it equals to 'ts':

https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L78

if in the future it would want to support tsx/unknown format, here would be it (it would likely need to handle the new parsing/compiling/defs anyways)


- PARSE.INDEX IS UNDOCUMENTED
i know it's type is inferred because of the default value but still interesting

https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L38


- AST PARSER
svelte compiler uses basic AST structure. obviously.


- `eat()` EMITS ERROR IF REQUIRED + NOT-LOOSE
`eat()` emits an expected token error if the expected token is not found and the function is set to required + non-loose (there are 2 mechanisms to determine if it's loose?)


- `eat()` DOESN'T EAT
for some reason, `eat()` doesn't actually eat the template, honestly acts like a weird wrapper to `match()`


- `element()`'S REGEX OF `regex_whitespace_or_slash_or_closing_tag` DOESN'T CHECK FOR TABS
the regex of `regex_whitespace_or_slash_or_closing_tag` will check only for a subsequent whitespace ( ), forward slash (/), or closing tag (>), meaning it will handle unique cases like tab (TAB)