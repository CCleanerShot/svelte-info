- ONLY MATCHES TS
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L78

svelte compiler's regex for checking the lang attribute only checks if it equals to 'ts'. if in the future it would want to support tsx/unknown format, here would be it (it would likely need to handle the new parsing/compiling/defs anyways)



- PARSE.INDEX IS UNDOCUMENTED
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L38

i know it's type is inferred because of the default value but still interesting, as it could mean its eventually a different type



- AST PARSER
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/index.js#L112

svelte compiler uses basic AST structure. obviously.



- `eat()` EMITS ERROR IF REQUIRED + NOT-LOOSE
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L181-L183

`eat()` emits an expected token error if the expected token is not found and the function is set to required + non-loose (there are 2 mechanisms to determine if it's loose?)



- `eat()` DOESN'T EAT
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L176-L179

`eat()` doesn't actually eat the template, it just increases the index



- `element()`'S REGEX OF `regex_whitespace_or_slash_or_closing_tag` DOESN'T CHECK FOR TABS
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L21

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
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/read/script.js#L37

uses the known library, "acorn" for parsing the script body



- REVERSED ATTRIBUTE NAMES
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/read/script.js#L48-L51

here is a list of reserved keywords for attributes that are not allowed:
'server', 'client', 'worker', 'test', 'default'



- COMMENTS NO ERROR HANDLING
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L57-L69

there doesn't seem like there is any error-handling once you eat a `!--` for a comment at a parsing level



- VOID ELEMENTS
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L78-L80

list of 'void' elements:
arguments
await
break
case
catch
class
const
continue
debugger
default
delete
do
else
enum
eval
export
extends
false
finally
for
function
if
implements
import
in
instanceof
interface
let
new
null
package
private
protected
public
return
static
super
switch
this
throw
true
try
typeof
var
void
while
with
yield



- SPECIAL EXCEPTION WITH VOID ELEMENTS
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L564

while not apart of the void list, when checking for if an name is a 'void' element, checks if the name is '!doctype' (or !DoCtYpE, might not matter atleast during parsing as it is never a closing tag)



- ONLY SYMBOL THAT SEPERATES AN ATTRIBUTE KEY
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/utils.js#L39-L41

`=` seems to be the only symbol that seperates an attribute key from it's attribute value 



- BASE ELEMENTS IMPLIED TO HAVE CHILDREN
https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L52-L335

all elements are implied (atleast during parsing) to have children, except for the following:
</> (closing tags), <!--COMMENT--> (comments), <script></script>, <style></style>


