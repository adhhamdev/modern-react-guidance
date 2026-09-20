# Migration & Codemods (React 18 → 19+)

## Recommended Order

1. Upgrade to latest React 18.3.x (adds deprecation warnings).
2. Fix all warnings.
3. Install React 19.x (prefer latest patch, currently 19.3+).
4. Run the official codemod recipe.
5. Fix remaining TypeScript issues.
6. Enable React Compiler if desired.
7. Adopt new APIs incrementally (Actions, `use`, View Transitions, etc.).

## Official Codemods

```bash
# Full recipe (recommended first pass)
npx codemod@latest react/19/migration-recipe

# Individual transforms
npx codemod react/19/remove-forward-ref --target .
npx codemod react/19/remove-context-provider --target .
npx codemod react/19/use-context-hook --target .
npx codemod react/19/replace-string-ref --target .
npx codemod react/19/replace-act-import --target .
npx codemod react/19/replace-reactdom-render --target .
# (and others listed in react-codemod)

# TypeScript types
npx types-react-codemod@latest preset-19 ./src
```

Source of truth: https://github.com/reactjs/react-codemod and the Codemod registry.

## Major Breaking Changes to Watch

- `ref` is now a regular prop → remove `forwardRef`.
- `Context.Provider` → just `<Context>`.
- `useContext` can become `use(Context)` (optional but preferred for consistency with `use`).
- String refs removed.
- Many legacy ReactDOM APIs removed (`findDOMNode`, `unmountComponentAtNode`, etc.).
- `defaultProps` on function components → JS default parameters.
- New JSX transform required.
- `react-test-renderer` deprecated → Testing Library.

## After Codemods

- Search for remaining `forwardRef`, `ReactDOM.render`, `element.ref`, `useEffect` that only fetches data.
- Add Suspense boundaries where `use(promise)` is introduced.
- Test forms thoroughly (Actions change reset and pending behavior).
- Verify third-party libraries that still expect old patterns.
