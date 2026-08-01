# Conditional Rendering

> Conditional rendering means displaying different UI based on a condition.

## Ternary Operator

Use when there are two possible UI states.

```tsx
{isLoggedIn ? (
  <Profile />
) : (
  <Login />
)}
```

Simple value:

```tsx
<Text>
  {isLoading ? "Loading..." : "Ready"}
</Text>
```

## Logical AND `&&`

Render something only when a condition is true.

```tsx
{isLoggedIn && <Profile />}
```

Example:

```tsx
{error && (
  <Text>{error}</Text>
)}
```

Be careful with numbers:

```tsx
// ⚠️ Can render 0
{count && <Text>{count}</Text>}

// ✅ Better
{count > 0 && <Text>{count}</Text>}
```

## Multiple Conditions

For complex conditions, calculate the result before JSX.

```tsx
let content;

if (isLoading) {
  content = <ActivityIndicator />;
} else if (error) {
  content = <Text>{error}</Text>;
} else {
  content = <Profile />;
}

return <View>{content}</View>;
```

## Early Return

Useful for loading/error states.

```tsx
if (isLoading) {
  return <ActivityIndicator />;
}

if (error) {
  return <Text>{error}</Text>;
}

return <Profile />;
```

## Quick Revision

```text
Condition
├── ? :       → Two possible states
├── &&        → Render when true
├── if        → Complex conditions
└── Early return → Loading/error states
```

> **Remember:** Keep conditional UI readable. For complex conditions, move logic outside the JSX.
