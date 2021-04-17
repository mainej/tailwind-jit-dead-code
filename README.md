# Problem

This repo demonstrates a problem with dead-code elimination in JIT watch mode.

# Reproduction steps

1. Run `npm install`
2. Run `NODE_ENV=development npx postcss ./styles.css -o ./compiled.css -w`
3. Observe that `compiled.css` contains `.bg-red-500`
4. In `index.html`, remove the `bg-red-500` class

## Expected

The `.bg-red-500` class is removed from `compiled.css`.

## Actual

`compiled.css` does not change.

# Comments

`index.html` is the only source file that references bg-red-500 (indeed, it's
the only source file period). Therefore, I expect that removing that class from
`index.html` would would remove it from the compiled css. However, there must
be some caching that keeps it around. In most cases it isn't a problem to have
extra style definitions in the compiled CSS, but it runs counter to the
advertised property that with the JIT, your development CSS is exactly the same
as your production CSS.
