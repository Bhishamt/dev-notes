# React

## Derive, don't sync

State that can be computed from props or other state should be computed during render. An effect that copies props into state runs one render late and shows a stale frame.

```tsx
// wrong: extra render, stale on first paint
useEffect(() => setFullName(first + " " + last), [first, last]);

// right
const fullName = first + " " + last;
```

## Reset state when a prop changes

Do it during render, not in an effect:

```tsx
if (prevUserId !== userId) {
  setPrevUserId(userId);
  setDraft("");
}
```

## Hooks

```tsx
const id = useId();                                  // stable id for label/input pairs
setCount(c => c + 1);                                // updater form — reads current state
const valueRef = useRef(0);                          // read inside timers/listeners
valueRef.current = value;                            // refs don't trigger renders
```

## Bugs that keep coming back

- `state` read immediately after `setState` is the old value. Use the updater form or compute locally.
- Missing `key` on a list puts row state on the wrong row after a reorder.
- `StrictMode` double-invokes effects in dev — if that breaks the code, the effect is not idempotent and it will break in production too.
- `useEffect` deps compare by reference. Wrapping a handler in `useCallback` only pays off when a memoized child depends on it.
- Subscribing without returning a cleanup leaks a listener per mount. Always return the unsubscribe.
