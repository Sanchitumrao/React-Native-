# Hooks

> Hooks are React functions that let functional components use state, effects, context, refs, and other React features.

## Common Hooks

```text
useState
useEffect
useContext
useRef
useMemo
useCallback
```

Custom hooks can also be created:

```text
useAuth
useFetch
useDebounce
useForm
```

---

## `useState`

Manages component state.

```tsx
const [count, setCount] = useState(0);

setCount(prev => prev + 1);
```

---

## `useEffect`

Runs side effects such as:

* API requests
* Subscriptions
* Timers
* Synchronizing with external systems

```tsx
useEffect(() => {
  fetchUser();
}, []);
```

Cleanup:

```tsx
useEffect(() => {
  const subscription = subscribe();

  return () => {
    subscription.unsubscribe();
  };
}, []);
```

---

## `useContext`

Reads values from React Context.

```tsx
const theme = useContext(ThemeContext);
```

Useful for shared values such as:

```text
Theme
Authentication
Language
App settings
```

---

## `useRef`

Stores a mutable value or references an element without causing a re-render when changed.

```tsx
const inputRef = useRef<TextInput>(null);

inputRef.current?.focus();
```

---

## `useMemo`

Memoizes a calculated value.

```tsx
const total = useMemo(() => {
  return calculateTotal(items);
}, [items]);
```

Use when a calculation is expensive or when referential stability matters.

---

## `useCallback`

Memoizes a function reference.

```tsx
const handlePress = useCallback(() => {
  submitForm();
}, []);
```

Useful when passing callbacks to memoized child components or when function identity matters.

---

## Custom Hooks

A custom hook extracts reusable stateful logic.

```tsx
function useCounter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(prev => prev + 1);
  };

  return { count, increment };
}
```

Usage:

```tsx
const { count, increment } = useCounter();
```

Custom hooks must start with `use`.

---

## Rules of Hooks

### 1. Call Hooks at the Top Level

```tsx
// ❌ Don't
if (isLoggedIn) {
  useEffect(() => {});
}
```

```tsx
// ✅ Do
useEffect(() => {
  if (isLoggedIn) {
    // logic
  }
}, [isLoggedIn]);
```

### 2. Call Hooks from React Functions

Hooks should be used inside:

* React components
* Custom hooks

Not regular JavaScript functions.

---

## Hook Selection

```text
Need local state?
    → useState

Need side effect?
    → useEffect

Need shared context?
    → useContext

Need persistent mutable reference?
    → useRef

Need expensive calculated value?
    → useMemo

Need stable function reference?
    → useCallback

Need reusable stateful logic?
    → Custom Hook
```

## Quick Revision

| Hook          | Main Purpose              |
| ------------- | ------------------------- |
| `useState`    | Component state           |
| `useEffect`   | Side effects              |
| `useContext`  | Read shared context       |
| `useRef`      | Mutable value / reference |
| `useMemo`     | Memoized value            |
| `useCallback` | Memoized function         |
| Custom Hook   | Reusable logic            |

> **Remember:** Hooks let functional components use React features. Use them based on a real requirement, not simply because they are available.
