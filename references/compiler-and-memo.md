# React Compiler & Memoization

## Detection

Look for:

- `babel-plugin-react-compiler` / `react-compiler` in dependencies or babel/webpack config
- `"reactCompiler": true` or similar in Next.js / Vite / Metro config
- Comments or eslint rules from the Compiler

If present → treat the project as Compiler-managed.

## Rules When Compiler Is On

1. Do **not** add new `useMemo`, `useCallback`, or `React.memo` for ordinary derived values or callbacks.
2. Existing manual memoization can remain during migration; do not expand it.
3. Still obey the Rules of React (pure components, no side effects during render, stable identities where required by third-party libs).
4. Use the Compiler Playground or eslint-plugin-react-hooks (Compiler rules) to verify.

## When Manual Memo Is Still Acceptable

- The value is passed to a non-React library that requires referential equality and the Compiler cannot see it.
- Measured performance regression after removing memo (rare).
- Library code that must ship without assuming the consumer runs the Compiler.

## Migration Tip

Run the Compiler in “annotation mode” or with gating first, then remove manual memo incrementally. Prefer deleting `useMemo`/`useCallback` once the Compiler covers the component.
