# React 19+ API Cheat Sheet

| API | Since | Purpose | Minimal Example |
|-----|-------|---------|-----------------|
| `use(promise \| context)` | 19.0 | Read resource in render (suspends) | `const data = use(fetchPromise)` |
| `useActionState` | 19.0 | Form/mutation state + pending | `[state, action, pending] = useActionState(fn, init)` |
| `useOptimistic` | 19.0 | Temporary optimistic UI | `[opt, addOpt] = useOptimistic(state)` |
| `useFormStatus` | 19.0 | Pending status of parent form | `const { pending } = useFormStatus()` |
| `ref` as prop | 19.0 | No more forwardRef | `function Input({ ref }) { ... }` |
| `<Context value={v}>` | 19.0 | No `.Provider` required | `<ThemeContext value={theme}>` |
| `useEffectEvent` | 19.2 | Non-reactive event from Effect | `const onX = useEffectEvent(() => ...)` |
| `<Activity mode>` | 19.2 | Hide + preserve state | `<Activity mode={vis ? 'visible' : 'hidden'}>` |
| `<ViewTransition>` | 19.3 | Native view transitions | `<ViewTransition enter="fade">` |
| `addTransitionType` | 19.3 | Tag a transition | `addTransitionType('nav')` |
| `browser()` | 19.3 | Browser-only subtree | `use(browser())` |
| Fragment refs | 19.3 | Ref on `<Fragment>` | `<Fragment ref={fragRef}>` |
| React Compiler | 19+ | Auto-memo | Enable in build; drop manual memo |

Always verify exact signatures on react.dev/reference.
