RANDOM STUFF:


- https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/read/script.js#L59 is kinda useless since this is implied with everything else around it lol


- https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L335 https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/state/element.js#L111 https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/phases/1-parse/index.js#L290-L293 2 links prior are used together to do this. very odd they decided to do it like this.


- https://github.com/CCleanerShot/svelte/blob/d8c6afde944a61c648c6b6f416f5ccafde272d44/packages/svelte/src/compiler/errors.js is generated by https://github.com/CCleanerShot/svelte/blob/7c6379a260799fdbecc43d9cb736ec9b81d21dec/packages/svelte/scripts/process-messages/index.js 


CHECKPOINT:
 ~~https://github.com/CCleanerShot/svelte/blob/1c2fc210232c16d2eb0fdb20d9bac3cef2b87897/packages/svelte/src/compiler/index.js#L22~~


TOTAL LINES: 91656


TODO:
DONE ~~- figure out why fucking source maps (either from vite or svelte's problem) are not actually being used, and im still using the original dumb source maps, meaning i cannot update them for testing (fucking cdn?)~~

IDK IM DUMB LOOK LATER ~~-  see if this PR can be extended + add tests for the existing codes: https://github.com/sveltejs/svelte/pull/15823/commits/9a3fcc4c334130f9472771094efed78b22f2ed8a~~

IDK IM DUMB LOOK LATER ~~- try to see what this PR does https://github.com/sveltejs/svelte/pull/15781~~