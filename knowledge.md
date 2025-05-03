- ONLY MATCHES TS
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L78

svelte compiler's regex for checking the lang attribute only checks if it equals to 'ts'. if in the future it would want to support tsx/unknown format, here would be it (it would likely need to handle the new parsing/compiling/defs anyways)



- PARSE.INDEX IS UNDOCUMENTED
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L38

i know it's type is inferred because of the default value but still interesting



- AST PARSER
svelte compiler uses basic AST structure. obviously.



- `eat()` EMITS ERROR IF REQUIRED + NOT-LOOSE
`eat()` emits an expected token error if the expected token is not found and the function is set to required + non-loose (there are 2 mechanisms to determine if it's loose?)



- `eat()` DOESN'T EAT
`eat()` doesn't actually eat the template, it just increases the index



- `element()`'S REGEX OF `regex_whitespace_or_slash_or_closing_tag` DOESN'T CHECK FOR TABS
the regex of `regex_whitespace_or_slash_or_closing_tag` will check only for a subsequent whitespace ( ), forward slash (/), or closing tag (>), meaning it will handle unique cases like tab (TAB)



- ODD `do () while` LOOP
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L73-L74

there is an odd do while loop here:
it seems to aggressively find the lang of the template before proceeding (never proceeding if it matches to a non-script tag)



- `/[\s=/>"']/` IS VALID REGEX
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L22

`/[\s=/>"']/` seems to be valid regex, despite regex101 refuting this. odd:



- LIST OF SYMBOLS THAT MATCH STATIC ATTRIBUTES
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L22

the list of symbols that will stop an attribute from being match seems to solely be this:
' ' (\s), '=', '>', '"', "'"



- ANY AMOUNT OF SPACES AFTER ATTRIBUTE DECLARATION
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L449-L450

you can set an any amount of spaces after declaring an attribute
example: <script lang=            "ts"></script> you're kinda weird if you do this tho



- PARSING STEP ANYTHING IS MATCHABLE
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L449-L451

during parsing, anything until the following is matchable for an attribute's value:
'>', ' ' (\s)



- `e.expected_token(parser.index, '=')` MISLEADING
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L474-L476

the error emitted here might be misleading, as it should not be expecting another =. this is just an illegal syntax to have a pair of quotes like this



- `this` ATTRIBUTE ALLOWED MULTIPLE TIMES
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L222-L227

seems like the `this` attribute is allowed to be multiple times (atleast during parsing), as it is explicitly checked against when checking for unique attribute names



- `acorn` FOR SCRIPT PARSING
uses the known library, "acorn" for parsing the script body





checkpoint:
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L451