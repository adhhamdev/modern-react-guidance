# Concurrent UX (React 19.2 / 19.3+)

## View Transitions (stable 19.3)

```tsx
import { ViewTransition, startTransition } from 'react';

function Panel({ open, children }) {
  return open ? (
    <ViewTransition enter="slide-in" exit="slide-out" share="morph">
      <div className="panel">{children}</div>
    </ViewTransition>
  ) : null;
}

// Trigger
startTransition(() => setOpen(true));
```

- Animations fire for updates inside `startTransition`, Suspense reveals, and `useDeferredValue`.
- Customize with CSS `::view-transition-old/new/group` or the event props (`onEnter`, `onExit`, `onShare`, `onUpdate`).
- `addTransitionType('navigation')` to tag a transition for CSS or JS control.
- Prefer native View Transitions over heavy animation libraries for route/page transitions when possible.

## Activity (stable 19.2)

```tsx
import { Activity } from 'react';

<Activity mode={isVisible ? 'visible' : 'hidden'}>
  <ExpensiveSidebar />
</Activity>
```

- `hidden` → `display: none`, destroys Effects, deprioritizes updates, but keeps state and DOM.
- Ideal for tabs, sidebars, pre-rendering next screens, or preserving form state across navigations.
- Combines cleanly with `<ViewTransition>` for enter/exit animations while state is preserved.

## useEffectEvent (stable 19.2)

```tsx
const onConnected = useEffectEvent(() => {
  showNotification('Connected!', theme); // always sees latest theme
});

useEffect(() => {
  const conn = createConnection(roomId);
  conn.on('connected', onConnected);
  return () => conn.disconnect();
}, [roomId]); // theme is NOT a dependency
```

Use only for “events” fired from Effects. Do not put reactive logic inside Effect Events.

## browser() (stable 19.3)

```tsx
import { use } from 'react';
import { browser } from 'react-dom';

function LocalOnly() {
  use(browser('Requires browser APIs'));
  return <div>{window.innerWidth}</div>;
}

// Must be under a Suspense boundary on the server
```

Replaces `typeof window` checks and hydration-mismatch-prone Effects.

## Deferred Values & Transitions

- `useDeferredValue(value)` for lagging UI (search results, filters).
- `startTransition` / `useTransition` for non-urgent state updates that should not block input.
