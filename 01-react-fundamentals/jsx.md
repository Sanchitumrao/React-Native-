# JSX

> JSX is a JavaScript syntax extension that allows you to describe UI using an HTML-like syntax inside JavaScript or TypeScript.

JSX is used extensively in React and React Native to define what a component should render.

---

## 📌 What is JSX?

JSX lets you write UI like this:

```tsx
function Welcome() {
  return (
    <View>
      <Text>Hello, React Native</Text>
    </View>
  );
}
```

Although JSX looks similar to HTML, it is **not HTML**.

React transforms JSX into JavaScript instructions that describe the UI.

```text
JS / TypeScript
      ↓
     JSX
      ↓
React transformation
      ↓
React elements
      ↓
UI
```

---

## 🧩 JSX in React Native

React Native does not use HTML elements such as:

```tsx
<div>
<p>
<button>
```

Instead, it provides native-oriented components:

```tsx
<View>
<Text>
<Pressable>
<TextInput>
<Image>
<ScrollView>
```

Example:

```tsx
import { View, Text, Pressable } from 'react-native';

function HomeScreen() {
  return (
    <View>
      <Text>Welcome</Text>

      <Pressable onPress={() => console.log('Pressed')}>
        <Text>Click Me</Text>
      </Pressable>
    </View>
  );
}
```

---

# 🏗️ Basic JSX Structure

```tsx
function Profile() {
  return (
    <View>
      <Text>Sanchit</Text>
      <Text>React Native Developer</Text>
    </View>
  );
}
```

A JSX element generally contains:

```text
Opening Tag
     ↓
Content
     ↓
Closing Tag
```

```tsx
<Text>Hello</Text>
```

Self-closing elements can be written as:

```tsx
<Image source={image} />
```

---

# 🔑 JSX Rules

## 1. Return a Single Root

A component must return one JSX tree.

❌ Incorrect:

```tsx
return (
  <Text>Hello</Text>
  <Text>World</Text>
);
```

✅ Correct:

```tsx
return (
  <View>
    <Text>Hello</Text>
    <Text>World</Text>
  </View>
);
```

You can also use a Fragment when appropriate:

```tsx
return (
  <>
    <Text>Hello</Text>
    <Text>World</Text>
  </>
);
```

In React Native, use a `View` when you actually need a native container or styling/layout behavior.

---

## 2. Close Every Element

❌ Incorrect:

```tsx
<Text>Hello
```

✅ Correct:

```tsx
<Text>Hello</Text>
```

Self-closing:

```tsx
<TextInput />
```

---

## 3. Use JavaScript Expressions with `{}`

Curly braces allow JavaScript expressions inside JSX.

```tsx
const name = 'Sanchit';

return (
  <Text>Hello {name}</Text>
);
```

Expressions can include:

```tsx
<Text>{user.name}</Text>

<Text>{count + 1}</Text>

<Text>{isLoggedIn ? 'Logout' : 'Login'}</Text>
```

---

# 🔄 JSX + JavaScript

JSX can be mixed with normal JavaScript logic.

```tsx
function UserProfile() {
  const name = 'Sanchit';
  const age = 22;

  return (
    <View>
      <Text>Name: {name}</Text>
      <Text>Age: {age}</Text>
    </View>
  );
}
```

Think of JSX as the **UI portion of your JavaScript/TypeScript code**, not as a separate language.

---

# 🎯 Expressions vs Statements

JSX accepts **expressions**, not arbitrary statements.

### Expressions

```tsx
<Text>{name}</Text>

<Text>{count + 1}</Text>

<Text>{isLoggedIn ? 'Welcome' : 'Login'}</Text>
```

### Statements

You cannot directly place statements such as `if` inside `{}`:

```tsx
// ❌ Invalid JSX
<Text>
  {if (isLoggedIn) {
    'Welcome'
  }}
</Text>
```

Instead, calculate the value before returning JSX:

```tsx
const message = isLoggedIn ? 'Welcome' : 'Please login';

return <Text>{message}</Text>;
```

Or use conditional rendering.

---

# 🔀 Conditional Rendering

## Ternary Operator

Useful when there are two possible UI states.

```tsx
<Text>
  {isLoggedIn ? 'Welcome back' : 'Please login'}
</Text>
```

For components:

```tsx
{isLoggedIn ? (
  <Profile />
) : (
  <Login />
)}
```

---

## Logical AND `&&`

Useful when something should render only when a condition is true.

```tsx
{isLoggedIn && <Profile />}
```

Example:

```tsx
{error && (
  <Text>
    {error}
  </Text>
)}
```

### Be careful with numeric values

```tsx
{count && <Text>{count}</Text>}
```

If `count` is `0`, the expression can produce an unexpected rendered `0`.

Prefer an explicit condition when needed:

```tsx
{count > 0 && <Text>{count}</Text>}
```

---

# 📋 Rendering Lists

JavaScript array methods can be used inside JSX.

```tsx
const users = ['Alex', 'John', 'Sam'];

return (
  <View>
    {users.map(user => (
      <Text key={user}>{user}</Text>
    ))}
  </View>
);
```

For larger React Native lists, prefer `FlatList` instead of manually rendering a large array with `.map()`.

```tsx
<FlatList
  data={users}
  keyExtractor={user => user.id}
  renderItem={({ item }) => (
    <Text>{item.name}</Text>
  )}
/>
```

---

# 🔑 JSX Keys

When rendering a list, React needs a stable `key` to identify individual elements.

```tsx
{users.map(user => (
  <Text key={user.id}>
    {user.name}
  </Text>
))}
```

### Good key

```tsx
key={user.id}
```

### Avoid

```tsx
key={Math.random()}
```

Random keys change between renders and can cause unnecessary remounting.

Using array indexes as keys should also be avoided when list items can be reordered, inserted, or deleted.

---

# 🎨 JSX Attributes and Props

JSX uses props to pass values to components.

```tsx
<TextInput
  placeholder="Enter your name"
  value={name}
  onChangeText={setName}
/>
```

For string values, quotes can be used:

```tsx
<Text>Hello</Text>
```

For JavaScript expressions, use `{}`:

```tsx
<Text>{name}</Text>
```

Boolean props can use shorthand:

```tsx
<Modal visible />
```

Equivalent to:

```tsx
<Modal visible={true} />
```

---

# 📦 Passing Objects and Arrays

JavaScript values can be passed through JSX expressions.

```tsx
<UserCard
  user={user}
  roles={roles}
/>
```

Functions can also be passed:

```tsx
<Button
  title="Save"
  onPress={handleSave}
/>
```

---

# 🧱 Nested JSX and `children`

Nested content is passed to a component through `children`.

```tsx
<Card>
  <Text>Profile</Text>
</Card>
```

Component:

```tsx
type CardProps = {
  children: React.ReactNode;
};

function Card({ children }: CardProps) {
  return (
    <View>
      {children}
    </View>
  );
}
```

This pattern is useful for reusable UI containers.

---

# 🔗 JSX and Components

Components can be used like custom JSX elements.

```tsx
function Header() {
  return (
    <View>
      <Text>My App</Text>
    </View>
  );
}
```

Use it inside another component:

```tsx
function HomeScreen() {
  return (
    <View>
      <Header />
      <Text>Home</Text>
    </View>
  );
}
```

### Naming matters

Custom components should start with an uppercase letter:

```tsx
<Header />
<UserCard />
<LoginForm />
```

Lowercase names are treated as native/intrinsic elements.

---

# 🧠 JSX and TypeScript

JSX works naturally with TypeScript in `.tsx` files.

```tsx
type UserProps = {
  name: string;
  age: number;
};

function User({ name, age }: UserProps) {
  return (
    <View>
      <Text>{name}</Text>
      <Text>{age}</Text>
    </View>
  );
}
```

### File extensions

```text
.ts   → TypeScript
.tsx  → TypeScript + JSX
.js   → JavaScript
.jsx  → JavaScript + JSX
```

For a TypeScript React Native project, `.tsx` is commonly used for components that contain JSX.

---

# ⚠️ JSX vs HTML

JSX may look like HTML, but React Native JSX represents React components rather than browser DOM elements.

| HTML       | React Native               |
| ---------- | -------------------------- |
| `<div>`    | `<View>`                   |
| `<p>`      | `<Text>`                   |
| `<button>` | `<Pressable>` / `<Button>` |
| `<input>`  | `<TextInput>`              |
| `<img>`    | `<Image>`                  |

React Native renders these components using the platform's native rendering system.

---

# 🚫 Common JSX Mistakes

## Missing Parent

```tsx
// ❌
return (
  <Text>Hello</Text>
  <Text>World</Text>
);
```

```tsx
// ✅
return (
  <View>
    <Text>Hello</Text>
    <Text>World</Text>
  </View>
);
```

---

## Forgetting `{}`

```tsx
const name = 'Sanchit';

// ❌
<Text>name</Text>

// ✅
<Text>{name}</Text>
```

---

## Calling a Function During Render

Be careful with event handlers.

```tsx
// ❌ Function executes immediately
<Pressable onPress={handlePress()}>
```

```tsx
// ✅ Pass the function
<Pressable onPress={handlePress}>
```

If arguments are required:

```tsx
<Pressable onPress={() => handlePress(id)}>
```

---

## Incorrect Component Naming

```tsx
// ❌
function userCard() {
  return <View />;
}
```

```tsx
// ✅
function UserCard() {
  return <View />;
}
```

Use PascalCase for React components.

---

# ⚡ JSX Performance Notes

JSX itself is usually not where you should start optimizing.

First focus on:

* Correct component structure
* Stable list keys
* Efficient `FlatList` usage
* Avoiding unnecessary state
* Avoiding unnecessary re-renders
* Keeping expensive calculations out of render when appropriate

Optimization tools such as:

```tsx
React.memo
useMemo
useCallback
```

should be used when there is a demonstrated need, rather than automatically everywhere.

---

# 🧪 Practical Example

A small React Native component combining common JSX concepts:

```tsx
import { useState } from 'react';
import {
  Pressable,
  Text,
  TextInput,
  View,
} from 'react-native';

function LoginForm() {
  const [email, setEmail] = useState('');
  const [isLoading, setIsLoading] = useState(false);

  const handleLogin = () => {
    setIsLoading(true);

    // Login logic...
  };

  return (
    <View>
      <Text>Login</Text>

      <TextInput
        placeholder="Email"
        value={email}
        onChangeText={setEmail}
      />

      <Pressable
        onPress={handleLogin}
        disabled={isLoading}
      >
        <Text>
          {isLoading ? 'Logging in...' : 'Login'}
        </Text>
      </Pressable>
    </View>
  );
}

export default LoginForm;
```

This example demonstrates:

```text
JSX
├── Components
├── Props
├── State
├── Expressions
├── Conditional Rendering
├── Event Handling
└── JavaScript inside JSX
```

---

# 📌 Quick Revision

```text
JSX
│
├── UI syntax inside JavaScript/TypeScript
├── React Native uses components instead of HTML elements
├── {} → JavaScript expressions
├── Props → Pass values to components
├── children → Nested JSX
├── ? : → Conditional UI
├── && → Render when condition is true
├── map() → Render small collections
├── key → Identify list items
└── .tsx → TypeScript + JSX
```

### Common Patterns

```tsx
// Expression
<Text>{name}</Text>

// Conditional
{isLoggedIn && <Profile />}

// Ternary
{isLoading ? <Loader /> : <Content />}

// Component
<UserCard name={name} />

// Event
<Pressable onPress={handlePress} />

// Function with argument
<Pressable onPress={() => handleDelete(id)} />

// Children
<Card>
  <Text>Hello</Text>
</Card>
```

---

# 🔑 Key Takeaways

1. **JSX describes the UI returned by React components.**
2. **JSX is JavaScript/TypeScript syntax, not HTML.**
3. Use `{}` to insert JavaScript expressions.
4. React Native JSX uses components such as `View`, `Text`, `Pressable`, and `TextInput`.
5. Use props to pass data between components.
6. Use conditional rendering to control what appears on screen.
7. Use stable keys when rendering lists.
8. Use `.tsx` for TypeScript files containing JSX.
9. Keep JSX readable and avoid putting excessive business logic directly inside it.
10. Optimize rendering only when there is a real performance problem.

> **Remember:** JSX describes **what the UI should look like**; state, props, and logic determine **what data that UI displays**.
