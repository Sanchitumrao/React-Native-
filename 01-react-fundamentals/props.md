# Props

> **Props (properties)** are read-only values passed from a parent component to a child component.

## Basic Example

```tsx
type UserProps = {
  name: string;
  age: number;
};

function UserCard({ name, age }: UserProps) {
  return (
    <View>
      <Text>{name}</Text>
      <Text>{age}</Text>
    </View>
  );
}
```

Usage:

```tsx
<UserCard name="Sanchit" age={22} />
```

## Data Flow

```text
Parent
   ↓
 Props
   ↓
Child
```

Props can contain:

```tsx
<User
  name="Sanchit"
  age={22}
  isActive={true}
  user={user}
  onPress={handlePress}
/>
```

## Props Are Read-Only

```tsx
// ❌ Don't mutate props
props.name = "New Name";
```

If the value needs to change, use **state** in the appropriate component.

## Passing Functions

Functions can be passed as props to allow a child to trigger parent logic.

```tsx
function Parent() {
  const handleDelete = () => {
    console.log("Deleted");
  };

  return <Child onDelete={handleDelete} />;
}
```

```tsx
function Child({ onDelete }: { onDelete: () => void }) {
  return (
    <Pressable onPress={onDelete}>
      <Text>Delete</Text>
    </Pressable>
  );
}
```

## `children`

Nested JSX is available through the `children` prop.

```tsx
function Card({ children }: { children: React.ReactNode }) {
  return <View>{children}</View>;
}
```

Usage:

```tsx
<Card>
  <Text>Hello</Text>
</Card>
```

## Quick Revision

```text
Props
├── Parent → Child
├── Read-only
├── Can contain values, objects, arrays, functions
├── Used to customize reusable components
└── children → Nested JSX
```

> **Remember:** Props pass data **into** a component; they should not be modified by the receiving component.
