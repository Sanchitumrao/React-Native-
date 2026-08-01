# Events

> Events allow React Native components to respond to user interactions such as taps, text input, scrolling, and gestures.

## Common Events

```text
onPress
onLongPress
onChangeText
onChange
onFocus
onBlur
onSubmitEditing
onScroll
```

## `onPress`

```tsx
<Pressable onPress={handlePress}>
  <Text>Press Me</Text>
</Pressable>
```

```tsx
const handlePress = () => {
  console.log("Pressed");
};
```

## Passing Arguments

Use an arrow function when arguments are required.

```tsx
<Pressable onPress={() => handleDelete(id)}>
  <Text>Delete</Text>
</Pressable>
```

Avoid:

```tsx
// ❌ Executes immediately during render
<Pressable onPress={handleDelete(id)}>
```

## `TextInput`

```tsx
const [name, setName] = useState("");

<TextInput
  value={name}
  onChangeText={setName}
  placeholder="Enter name"
/>
```

`onChangeText` receives the updated text directly.

## Event + State

Events commonly update state.

```tsx
const [count, setCount] = useState(0);

<Button
  title="Add"
  onPress={() => setCount(prev => prev + 1)}
/>
```

Flow:

```text
User Action
    ↓
Event Handler
    ↓
State Update
    ↓
Re-render
    ↓
Updated UI
```

## Passing Event Handlers as Props

```tsx
<CustomButton onPress={handleSubmit} />
```

Child:

```tsx
function CustomButton({
  onPress,
}: {
  onPress: () => void;
}) {
  return (
    <Pressable onPress={onPress}>
      <Text>Submit</Text>
    </Pressable>
  );
}
```

## Common Mistakes

```tsx
// ❌ Calling immediately
onPress={handleSubmit()}

// ✅ Passing function
onPress={handleSubmit}

// ✅ Passing arguments
onPress={() => handleSubmit(id)}
```

## Quick Revision

```text
Event
├── User interaction
├── Handler function responds
├── Handler may update state
└── State update → UI re-render
```

> **Remember:** Pass a function to an event prop. Use `() => ...` when you need to provide arguments or additional logic.
