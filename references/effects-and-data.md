# Effects & Data Fetching

## You Might Not Need an Effect (Codified)

| Goal | Prefer instead of Effect |
|------|--------------------------|
| Derive value from props/state | Compute during render |
| Reset state when prop changes | `key={prop}` on the component or compute |
| Notify parent of state change | Call the parent callback in the event handler |
| Fetch data | `use(promise)` + Suspense (or library that integrates with Suspense) |
| Subscribe to external store | `useSyncExternalStore` |
| Run code on mount only | Rarely needed; prefer event handlers or layout effects carefully |

Only keep an Effect when you are synchronizing with an external system that React does not know about (DOM measurements that must happen after paint, third-party widgets, WebSocket that is not data, etc.). Always return a cleanup function.

## Modern Data Fetching

```tsx
// Parent (or framework loader) creates the promise
const commentsPromise = fetchComments(postId);

function Page() {
  return (
    <Suspense fallback={<Skeleton />}>
      <Comments commentsPromise={commentsPromise} />
    </Suspense>
  );
}

function Comments({ commentsPromise }) {
  const comments = use(commentsPromise); // can be conditional
  return comments.map(...);
}
```

- Never create the promise inside the component that calls `use` (caching required).
- Frameworks (Next.js, Remix, etc.) usually provide the cached promise for you.
- For client-only libraries, prefer ones that integrate with Suspense / `use`.

## useEffectEvent Reminder

Extract non-reactive logic that should always see the latest props/state but should not re-subscribe the Effect.
