# Module Resolution in TypeScript

```ts
import {a} from "moduleA"
```
__moduleA is a non-relative reference.__

1. The compiler will try to locate the file using one of two different strategies: [Classic](#classic) or [Node](#node).
2. If number one didn't work and the module name is no-relative, then the compiler will attempt to locate an __ambient module declaration__.

## Relative vs Non-relative module imports

Module imports are resolved differently based on whether the module reference is relative or non-relative.

A _relative import_ in one that starts with `/`, `./`, `../`. Any other import is considered __non-relative__.

A relative import is resolve relative to the importing file and _cannot_ resolve to an ambient module declaration.

A non-relative import can be resolved relative to `baseUrl`, or through path mapping. They can also resolve to __ambient module declarations__.

### Module Resolution Strategies

There are two possible module resolution strategies: [Node](#node) and [Classic](#classic). You can use the `--moduleResolution` flag to specify the module resolution strategy. If not specified, the default is [Classic](#classic) for `--modude AMD | System | ES2015` or [Node](#node) otherwise.

## Classic
This used to be TypeScript's default resolution strategy. Nowadays, this strategy is mainly present for backward compatibility.

A relative import will be resolved relative to the importing file. So `import {b} from "./moduleB"` in source file `/root/src/folder/A.ts` would result in the following lookups:

1. `/root/src/folder/moduleB.ts` 
2. `/root/src/folder/moduleB.d.ts` 

For non-relative module imports, however, the compiler walks up the directory tree starting with the directory containing the importing file, trying to locate a matching definition file.

Using the previous example but importing with `import {b} from "moduleB"`:

1. `/root/src/folder/moduleB.ts`
2. `/root/src/folder/moduleB.d.ts`
3. `/root/src/moduleB.ts`
4. `/root/src/moduleB.d.ts`
5. `/root/moduleB.ts`
6. `/root/moduleB.d.ts`
7. `/moduleB.ts`
8. `/moduleB.d.ts`

## Node
This resolution strategy attempts to mimic the [Node.js](https://nodejs.org) module resolution mechanism at runtime. The full Node.js resolution algorithm is outline in [Node.js module documentation](https://nodejs.org/api/modules.html#modules_all_together).

### How Node.js resolves modules
Imports in Node.js are performed by calling a function named `require`. The behavior Node.js takes will differ depending on if `require` is given a relative path or a non-relative path.

Relative paths are straightforward. As an example, let's consider a file located at `/root/src/moduleA.js`, which contains the import `var x = require("./moduleB")`; Node.js resolves that import in the following order:

1. Ask the file named `/root/src/moduleB.js`, if it exists.
2. Ask the folder `/root/src/moduleB`, if it contains a file named `package.json` that specifies a `"main"` module. In our example, if Node.js found the file `/root/src/moduleB/package.json` containing `{ "main": "lib/mainModule.js" }` the node will refer to `/root/src/moduleB/lib/mainModule.js`.
3. Ask the folder `/root/src/moduleB` if it contains a file named `ìndex.js`. That file is implicitly considered that folder's "main" module.

However, resolution for a [non-relative module name](#relative-vs-non-relative-module-imports) is performed differently. Node will look for your modules in special folders named `node_modules`. A `node_modules` folder can be on the same level as the current file, or higher up in the directory chain. Node will walk up the directory chain, looking through each `node_modules` until it finds the module your tried to load.

For example consider: `/root/src/moduleA.js` had the import `var x = require("moduleB")`. Node would then try to resolve `moduleB` to each locations until one worked.

1. `/root/src/node_modules/moduleB.js`
2. `/root/src/node_modules/moduleB/package.json` (if it specifies a "main" property)
3. `/root/src/node_modules/moduleB/index.js`
<br/><br />
4. `/root/node_modules/moduleB.js`
5. `/root/node_modules/moduleB/package.json` (if it specifies a "main" property)
6. `/root/node_modules/moduleB/index.js`
<br/><br />
7. `/node_modules/moduleB.js`
8. `/node_modules/moduleB/package.json` (if it specifies a "main" property)
9. `/node_modules/moduleB/index.js`

### How TypeScript resolves modules
TypeScript will mimic the Node.js run-time resolution strategy in order to locate definition files for modules at compile-time. To accomplish this, TypeScript overlays the TypeScript source file extensions (`.ts`, `.tsx`, and `.d.ts`) over the Node's resolution logic. TypeScript will also use a field in `package.json` named `"types"` to mirror the purpose of `"main"` - the compiler will use it to find the "main" definition file to consult.

So for `import {b} from "./moduleB"` TypeScript would attempt the following locations:

1. `/root/src/moduleB.ts`
2. `/root/src/moduleB.tsx`
3. `/root/src/moduleB.d.ts`
4. `/root/src/moduleB/package.json` (if it specifies a "types" property)
5. `/root/src/moduleB/index.ts`
6. `/root/src/moduleB/index.tsx`
7. `/root/src/moduleB/index.d.ts`

Similarly a non-relative import will follow the Node.js resolution logic, first looking up a file, then looking up an applicable folder. So `import {b} from "moduleB"` would result in the following lookups:

1. `/root/src/node_modules/moduleB.ts`
2. `/root/src/node_modules/moduleB.tsx`
3. `/root/src/node_modules/moduleB.d.ts`
4. `/root/src/node_modules/moduleB/package.json` (if it specifies a "types" property)
5. `/root/src/node_modules/moduleB/index.ts`
6. `/root/src/node_modules/moduleB/index.tsx`
7. `/root/src/node_modules/moduleB/index.d.ts`
<br/><br/>
8. `/root/node_modules/moduleB.ts`
9. `/root/node_modules/moduleB.tsx`
10. `/root/node_modules/moduleB.d.ts`
11. `/root/node_modules/moduleB/package.json` (if it specifies a "types" property)
12. `/root/node_modules/moduleB/index.ts`
13. `/root/node_modules/moduleB/index.tsx`
14. `/root/node_modules/moduleB/index.d.ts`
<br/><br/>
15. `/node_modules/moduleB.ts`
16. `/node_modules/moduleB.tsx`
17. `/node_modules/moduleB.d.ts`
18. `/node_modules/moduleB/package.json` (if it specifies a "types" property)
19. `/node_modules/moduleB/index.ts`
20. `/node_modules/moduleB/index.tsx`
21. `/node_modules/moduleB/index.d.ts`

## Additional module resolution flags

TypeScript has a set of additional flags to _inform_ the compiler of transformations that are expected to happen to the sources to generate the final output.

It is important to note that the compiler will _not_ perform any of these transformation; it just uses these pieces of information to guide the process of resolving a module import to its definition file.

### Base URL

Using a `baseUrl` is a common practice in applications using AMD module loaders where modules are "deployed" to a single folder at run-time. The sources of these modules can live in different directories, but a build script will put them all together.

Setting `baseUrl` informs the compiler where to find modules. All module imports with non-relative names are assumed to be relative to the `baseUrl`.

Values of _baseUrl_ is determined as either:

* value of _baseUrl_ command line argument (if given path is relative, it is computed based on current directory)
* value of _baseUrl_ property in 'tsconfig.json' (if given path is relative, it is computed based on the location of 'tsconfig.json')

Note that relative module imports are not impacted by setting the baseUrl, as they are always resolved relative to their importing files.

### Path mapping
Sometimes modules are not directly located under _baseUrl_. For instance, an import to a module `"jquery"` would be translated at runtime to `"node_modules/jquery/dist/jquery.slim.min.js"`. Loaders use a mapping configuration to map modules names to files at run-time.

The TypeScript compiler supports the declaration of such mappings using `"paths"` property in `tsconfig.json` files. Here is an example for how to specify the `"paths"` property for `jquery`.

```json
{
  "compilerOptions": {
    "baseUrl": ".", // this must be specified if "paths" is.
    "paths": {
      "jquery": ["node_modules/jquery/dist/jquery"] // this mapping is relative to "baseUrl"
    }
  }
}
```
Please note that `"paths"` are resolved relative to `"baseUrl"`. When setting `"baseUrl"` to another value than `"."`, i.e. the directory of `tsconfig.json`, the mappings must be changed accordingly. Say you set `"baseUrl": "./src"` in the above example, then jquery should be mapped to `"../node_modules/jquery/dist/jquery"`.

Using `"paths"` also allows for more sophisticated mappings including multiple fall back locations. Consider a project configuration where only some modules are available in one location, and the rest are in another. A build step would put them all together in one place. The project layout may look like:

```tree
projectRoot
├── folder1
│   ├── file1.ts (imports 'folder1/file2' and 'folder2/file3')
│   └── file2.ts
│
├── generated
│   ├── folder1
│   └── folder2
│       └── file3.ts
└── tsconfig.json
```

The corresponding `tsconfig.json` would look like:

```json
{
  "compilerOptions": {
    "baseUrl": ".", // same location of tsconfig.json 
    "paths": {
      "*": [
        "*",
        "generated/*"
      ]
    }
  }
}
```

This tells the compiler for any module import that matches the pattern `"*"` (i.e. all values), to look in two locations:

1. `"*"`: meaning the same name unchanged, so map `<moduleName>` => `<baseUrl>/<moduleName>`.
2. `"generated/*"` meaning the module name with an appended prefix "generated", so map `<moduleName>` => `<baseUrl>/generated/<moduleName>`.

Following this logic, the compiler will attempt to resolve the two imports as such:
* import 'folder1/file2'
    1. pattern '*' is matched and wildcard captures the whole module name.
    2. try first substitution in the list '*' -> `folder1/file2`.
    3. result of substitution is non-relative name - combine it with _baseUrl_ -> `project/folder1/file2.ts`.
    4. File exists. Done.
* import 'folder2/file3'
    1. pattern '*' is matched and wildcard captures the whole module name.
    2. try first substitution in the list '*' -> `folder2/file3`.
    3. result of substitution is non-relative name - combine it with _baseUrl_ -> `project/folder2/file3.ts`.
    4. file does not exists, move to the second substitution.
    5. second substitution 'generated/*' -> `generated/folder2/file3`.
    6. result of substitution is non-relative name - combine it with _baseUrl_ -> `projectRoot/generated/folder2/file3.ts`.
    7. file exists. Done.

### Virtual Directories with `rootDirs`
