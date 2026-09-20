# Actions & Forms (React 19+)

## Core Pattern

```tsx
import { useActionState, useOptimistic } from 'react';
import { useFormStatus } from 'react-dom';

async function updateNameAction(prevState: string | null, formData: FormData) {
  const name = formData.get('name') as string;
  const error = await saveName(name); // your mutation
  if (error) return error;
  return null;
}

function NameForm({ currentName }: { currentName: string }) {
  const [error, formAction, isPending] = useActionState(updateNameAction, null);
  const [optimisticName, setOptimisticName] = useOptimistic(currentName);

  const action = async (formData: FormData) => {
    const name = formData.get('name') as string;
    setOptimisticName(name);
    return formAction(formData);
  };

  return (
    <form action={action}>
      <p>Current: {optimisticName}</p>
      <input name="name" disabled={isPending} />
      <SubmitButton />
      {error && <p role="alert">{error}</p>}
    </form>
  );
}

function SubmitButton() {
  const { pending } = useFormStatus();
  return <button type="submit" disabled={pending}>Save</button>;
}
```

## Key Rules

- Pass an async function (Action) to `action` / `formAction` on `<form>`, `<button>`, or `<input>`.
- `useActionState(action, initialState, permalink?)` returns `[state, dispatch, isPending]`.
- `useFormStatus()` must be called from a component rendered *inside* the form (reads nearest form status).
- `useOptimistic(state, updateFn?)` shows temporary UI; React reverts on error or when real state catches up.
- Uncontrolled forms auto-reset on successful Action. Call `requestFormReset(form)` if you need manual control.
- Server Actions (when the framework supports them) work with the exact same hooks.

## Common Pitfalls

- Do not mix controlled inputs with form Actions unless necessary; prefer uncontrolled + FormData.
- Do not manually manage `isPending` when using `useActionState` or `useTransition`.
- `useFormStatus` only works for the parent form; it is not a global store.
