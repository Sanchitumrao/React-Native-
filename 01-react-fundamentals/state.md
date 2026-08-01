# State

> **State** is data managed by a component that can change over time and cause the UI to update.

## `useState`

```tsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <View>
      <Text>{count}</Text>

      <Button
        title="Add"
        onPress={() => setCount(prev => prev + 1)}
      />
    </View>
  );
}
```

```text
count     → current state
setCount  → update function
0         → initial value
```

## Updating State

Use the setter instead of modifying state directly.

```tsx
// ❌ Don't
count = count + 1;

// ✅ Do
setCount(prev => prev + 1);
```

For updates based on previous state, prefer the functional form:

```tsx
setCount(prev => prev + 1);
```

## Objects

```tsx
const [user, setUser] = useState({
  name: "",
  age: 0,
});

setUser(prev => ({
  ...prev,
  name: "Sanchit",
}));
```

## Arrays

```tsx
const [items, setItems] = useState<string[]>([]);

setItems(prev => [...prev, "React Native"]);
```

Remove an item:

```tsx
setItems(prev => prev.filter(item => item !== "React Native"));
```

## State vs Props

```text
Props
Parent → Child
Read-only from child

State
Owned by component
Can change
Triggers re-render
```

## Important Rules

* Never mutate state directly.
* Keep state as local as possible.
* Don't create state for values that can be calculated from existing data.
* Use functional updates when the new value depends on the previous value.
* Avoid storing duplicated/derived data unnecessarily.

## Quick Revision

```text
State
├── Component-managed data
├── Can change over time
├── useState → simple state
├── setState → update state
├── State update → re-render
└── Never mutate directly
```

> **Remember:** State represents data that can change and affect what the component displays.
