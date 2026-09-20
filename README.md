# Modern React Guidance

**Authoritative agent skill for React 19+**

Optimized for AI coding agents (Claude Code, Cursor, Codex, Copilot, etc.).

Inspired by the proposal in [reactwg/async-react#12](https://github.com/reactwg/async-react/discussions/12) and structured after high-quality skills from Vercel, Callstack, and Margelo.

## What it covers

- React 19 / 19.1 / 19.2 / 19.3+ features
- Actions, `useActionState`, `useOptimistic`, `useFormStatus`
- `use()` + Suspense for data
- React Compiler (trust it, drop unnecessary manual memo)
- `<ViewTransition>` (stable in 19.3)
- Fragment refs
- `<Activity>`
- `useEffectEvent`
- `browser()` from `react-dom`
- Official codemods for React 19 migration
- “You Might Not Need an Effect” rules

## Install

### Via skills.sh / agent skills CLI

```bash
npx skills add adhhamdev/modern-react-guidance
```

(or the equivalent install command for your agent)

### Manual

Copy the `modern-react-guidance/` folder into your agent’s skills directory.

## Structure

```
modern-react-guidance/
├── SKILL.md                    # Core instructions (always loaded when triggered)
└── references/
    ├── actions-and-forms.md
    ├── api-cheatsheet.md
    ├── compiler-and-memo.md
    ├── concurrent-ux.md
    ├── effects-and-data.md
    └── migration-codemods.md
```

## Author

**Adhham** — [adhham.dev](https://adhham.dev)

## License

MIT
