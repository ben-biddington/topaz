## The -d option omits directories

Reported [here](https://github.com/swc-project/swc/issues/2092)

This is a simplified example: normally I have several directories in the root that I'd want included.

I find that when using [the `-d` flag](https://swc.rs/docs/usage/cli#--out-dir--d), the output is missing some directories. 

Given these source files:

```
core/
└── sample
    └── a.ts
```

when I run 

```
npx swc **/**/*.ts -d $PWD/dist
```

I expect this result in `dist`:

```
dist/
└── core/
    └── sample
        └── a.js
```

Instead, `core` is omitted:

```
dist/
└── sample
    └── a.js
```

### Tried different glob (same result)

`**/**/*.ts` -> `$PWD`

```
npx swc $PWD -d $PWD/dist && tree --noreport dist
Successfully compiled: 2 files with swc (113.74ms)
dist
└── sample
    └── a.js

```

Is there a flag I am missing?

[Related?](https://github.com/swc-project/swc/blob/main/crates/swc_cli/src/commands/compile.rs#L176)
