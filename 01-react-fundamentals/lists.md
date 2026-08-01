# Lists

> Lists display collections of data. React Native provides `FlatList` and `SectionList` for efficient list rendering.

## `map()`

Useful for small, simple collections.

```tsx
const names = ["Alex", "John", "Sam"];

{names.map(name => (
  <Text key={name}>{name}</Text>
))}
```

Always provide a stable `key`.

```tsx
key={item.id}
```

Avoid:

```tsx
key={Math.random()}
```

## `FlatList`

Recommended for most dynamic or larger lists.

```tsx
<FlatList
  data={users}
  keyExtractor={item => item.id}
  renderItem={({ item }) => (
    <Text>{item.name}</Text>
  )}
/>
```

### Important Props

```tsx
<FlatList
  data={data}
  renderItem={renderItem}
  keyExtractor={item => item.id}
  ListEmptyComponent={<Text>No data</Text>}
  refreshing={refreshing}
  onRefresh={handleRefresh}
/>
```

## `SectionList`

Use when data is grouped into sections.

```tsx
<SectionList
  sections={sections}
  keyExtractor={item => item.id}
  renderItem={({ item }) => (
    <Text>{item.name}</Text>
  )}
  renderSectionHeader={({ section }) => (
    <Text>{section.title}</Text>
  )}
/>
```

Data structure:

```tsx
const sections = [
  {
    title: "Students",
    data: students,
  },
  {
    title: "Teachers",
    data: teachers,
  },
];
```

## `FlatList` vs `ScrollView`

```text
ScrollView
└── Renders all children
    → Good for small content

FlatList
└── Virtualized list rendering
    → Better for large/dynamic lists
```

Avoid putting a large list inside a `ScrollView` unless there is a specific reason.

## Common Mistakes

```text
❌ Missing stable keys
❌ Using random keys
❌ Rendering huge lists with map()
❌ Using ScrollView for large datasets
❌ Putting complex logic inside renderItem
```

## Quick Revision

```text
Lists
├── map()       → Small collections
├── FlatList    → Most dynamic lists
├── SectionList → Grouped lists
├── key         → Stable item identity
└── renderItem  → Defines list item UI
```

> **Remember:** For real React Native applications, `FlatList` should be your default choice for dynamic lists.
