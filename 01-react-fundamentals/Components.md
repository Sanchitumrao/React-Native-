# React Components

> Components are the building blocks of React and React Native applications. They allow you to split a UI into small, reusable, and maintainable pieces.

---

## 📌 What Is a Component?

A React component is a reusable piece of UI that:

* Receives data through **props**
* Can manage data through **state**
* Returns UI using **JSX**
* Can contain logic and event handlers
* Can be composed with other components

In modern React, components are usually written as **functions**.

```tsx
function Welcome() {
  return <Text>Welcome!</Text>;
}
```

In React Native:

```tsx
import { View, Text } from 'react-native';

function Welcome() {
  return (
    <View>
      <Text>Welcome!</Text>
    </View>
  );
}

export default Welcome;
```

---

# 🧩 Component Structure

A typical component can contain:

```text
Component
│
├── Imports
├── Props
├── State
├── Event Handlers
├── Logic
└── JSX / UI
```

Example:

```tsx
import { useState } from 'react';
import { Button, Text, View } from 'react-native';

type CounterProps = {
  initialValue?: number;
};

function Counter({ initialValue = 0 }: CounterProps) {
  const [count, setCount] = useState(initialValue);

  const increment = () => {
    setCount(prev => prev + 1);
  };

  return (
    <View>
      <Text>Count: {count}</Text>
      <Button title="Increment" onPress={increment} />
    </View>
  );
}

export default Counter;
```

---

# 🏗️ Types of Components

## 1. Functional Components

The standard approach for modern React.

```tsx
function Greeting() {
  return <Text>Hello</Text>;
}
```

Arrow-function style:

```tsx
const Greeting = () => {
  return <Text>Hello</Text>;
};
```

Both are valid.

---

## 2. Reusable Components

A component should be reusable when the same UI or behavior appears in multiple places.

```tsx
function PrimaryButton({ title, onPress }: Props) {
  return (
    <Pressable onPress={onPress}>
      <Text>{title}</Text>
    </Pressable>
  );
}
```

Usage:

```tsx
<PrimaryButton
  title="Login"
  onPress={handleLogin}
/>

<PrimaryButton
  title="Register"
  onPress={handleRegister}
/>
```

---

# 📦 Props

Props allow a parent component to pass data to a child component.

### Parent

```tsx
<UserCard
  name="Sanchit"
  age={22}
/>
```

### Child

```tsx
type UserCardProps = {
  name: string;
  age: number;
};

function UserCard({ name, age }: UserCardProps) {
  return (
    <View>
      <Text>{name}</Text>
      <Text>{age}</Text>
    </View>
  );
}
```

### Remember

```text
Parent
   ↓
 Props
   ↓
Child
```

Props are **read-only** from the child's perspective.

---

# 🔄 State Inside Components

Components can maintain their own state using hooks such as `useState`.

```tsx
const [count, setCount] = useState(0);
```

Example:

```tsx
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

State changes cause the component to render again with the updated value.

---

# 👨‍👩‍👦 Parent and Child Components

Components can be nested.

```tsx
function App() {
  return (
    <View>
      <Header />
      <Profile />
      <Footer />
    </View>
  );
}
```

Conceptually:

```text
App
│
├── Header
├── Profile
└── Footer
```

This makes large applications easier to organize.

---

# 🔁 Passing Data Down

Data normally flows from parent to child through props.

```text
Parent
   │
   │ props
   ↓
Child
```

Example:

```tsx
function App() {
  const username = 'Sanchit';

  return <Profile name={username} />;
}
```

```tsx
function Profile({ name }: { name: string }) {
  return <Text>{name}</Text>;
}
```

---

# ⬆️ Passing Data Up

Children cannot directly modify the parent's state.

Instead, the parent can pass a function as a prop.

### Parent

```tsx
function App() {
  const handleMessage = (message: string) => {
    console.log(message);
  };

  return <Child onMessage={handleMessage} />;
}
```

### Child

```tsx
function Child({
  onMessage,
}: {
  onMessage: (message: string) => void;
}) {
  return (
    <Button
      title="Send"
      onPress={() => onMessage('Hello from child')}
    />
  );
}
```

Flow:

```text
Parent
  ↓
function prop
  ↓
Child
  ↓
calls function
  ↓
Parent logic
```

---

# 🧱 Component Composition

Instead of creating one huge component, combine smaller components.

```tsx
function HomeScreen() {
  return (
    <View>
      <Header />
      <SearchBar />
      <ProductList />
      <BottomNavigation />
    </View>
  );
}
```

This is **component composition**.

### Good structure

```text
HomeScreen
├── Header
├── SearchBar
├── ProductList
│   └── ProductCard
└── BottomNavigation
```

---

# 🧩 `children` Prop

Components can accept nested content through `children`.

```tsx
function Card({ children }: { children: React.ReactNode }) {
  return (
    <View>
      {children}
    </View>
  );
}
```

Usage:

```tsx
<Card>
  <Text>Hello</Text>
</Card>
```

This is useful for reusable containers such as:

* Cards
* Modals
* Sections
* Layout wrappers
* Custom UI components

---

# 🎨 Component + Styling

Keep reusable components responsible for their own basic presentation.

```tsx
const Button = ({ title, onPress }: Props) => {
  return (
    <Pressable style={styles.button} onPress={onPress}>
      <Text style={styles.text}>{title}</Text>
    </Pressable>
  );
};
```

Avoid duplicating the same UI code throughout the application.

---

# 🗂️ Component Organization

A common project structure:

```text
src/
│
├── components/
│   ├── Button/
│   │   ├── Button.tsx
│   │   └── styles.ts
│   │
│   ├── Card/
│   │   ├── Card.tsx
│   │   └── styles.ts
│   │
│   └── Input/
│       ├── Input.tsx
│       └── styles.ts
│
├── screens/
├── navigation/
├── hooks/
├── services/
└── utils/
```

For smaller projects, a simpler structure is also fine.

---

# 🧠 Smart vs Presentational Components

A useful conceptual distinction:

### Presentational Component

Primarily responsible for UI.

```tsx
<UserCard
  name={user.name}
  email={user.email}
/>
```

### Logic / Container Component

Handles data, state, API calls, or business logic.

```tsx
function UserScreen() {
  const [user, setUser] = useState<User | null>(null);

  // Fetch user...

  return <UserCard name={user?.name} email={user?.email} />;
}
```

Modern React does not require a strict separation, but keeping complex logic organized makes applications easier to maintain.

---

# ⚡ Component Re-rendering

A component can render again when:

* Its state changes
* Its parent renders
* Its props change
* A consumed context value changes

Example:

```tsx
const [count, setCount] = useState(0);

setCount(count + 1);
```

The component renders again using the new state.

> A re-render does **not** automatically mean the entire application is rebuilt from scratch.

---

# 🚫 Common Mistakes

### 1. Making Components Too Large

Avoid:

```text
One screen
├── UI
├── API calls
├── validation
├── navigation
├── business logic
├── storage
└── everything else
```

Prefer breaking complex screens into logical components and services.

---

### 2. Duplicating UI

Avoid writing the same button repeatedly.

```tsx
<Pressable>...</Pressable>
<Pressable>...</Pressable>
<Pressable>...</Pressable>
```

Create a reusable component when the UI pattern is genuinely repeated.

---

### 3. Mutating Props

Don't modify props directly.

```tsx
// ❌ Don't
props.name = 'New Name';
```

Props should be treated as read-only.

---

### 4. Using State Unnecessarily

Not every value needs state.

```tsx
// Usually unnecessary
const [fullName, setFullName] = useState(
  `${firstName} ${lastName}`
);
```

If a value can be calculated from existing state/props, it often doesn't need its own state.

---

### 5. Creating Components Inside Components Unnecessarily

Avoid defining reusable components inside another component when there is no strong reason.

```tsx
function Screen() {
  function Card() {
    return <View />;
  }

  return <Card />;
}
```

Prefer:

```tsx
function Card() {
  return <View />;
}

function Screen() {
  return <Card />;
}
```

This can make component identity and performance behavior easier to reason about.

---

# ✅ Component Design Checklist

Before creating a component, ask:

* [ ] Is this UI reused?
* [ ] Does it have a clear responsibility?
* [ ] Are props clearly defined?
* [ ] Is local state actually required?
* [ ] Can the component be tested independently?
* [ ] Is the component becoming too large?
* [ ] Is business logic unnecessarily mixed with UI?
* [ ] Is the name descriptive?
* [ ] Is the component easy to reuse?

---

# 📌 Quick Revision

| Concept              | Remember                                       |
| -------------------- | ---------------------------------------------- |
| Component            | Reusable UI building block                     |
| Functional Component | Modern component style                         |
| Props                | Data passed from parent                        |
| State                | Component-managed changing data                |
| Children             | Nested content passed to a component           |
| Composition          | Building UI from smaller components            |
| Parent → Child       | Data through props                             |
| Child → Parent       | Callback function through props                |
| Re-render            | Component renders again after relevant changes |
| Reusable Component   | UI/behavior designed for repeated use          |

---

# 🔑 Key Takeaways

```text
Component
    ↓
Reusable UI + Logic
    ↓
Props → Receive Data
    ↓
State → Manage Changing Data
    ↓
Events → Respond to User Actions
    ↓
Composition → Build Larger UIs
```

### Remember

> **Build small, focused components. Pass data through props. Keep state where it belongs. Compose components to create larger screens.**
