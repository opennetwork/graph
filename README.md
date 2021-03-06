# Graph

See [tsgraph](https://github.com/opennetwork/tsgraph)

```typescript
export interface ReadonlyGraph extends ReadonlyDataset<Quad> {
  [Symbol.iterator](): Iterator<Quad>
  [Symbol.asyncIterator](): AsyncIterator<[ReadonlyDataset<Quad>, ReadonlyDataset<Quad>]>
  subject: BlankNode | NamedNode | Variable
}
```

```typescript
export interface Graph extends ReadonlyGraph {
  add(quad: Quad): void
  // Add anything, we will try and figure out the context
  // If the input is unresolvable an error will be thrown with a clear reason as to why not
  add(unknown: unknown): void
}
```

```typescript
export interface GraphFunction<Q extends Quad = Quad, Variables extends unknown[]> {
  (this: ReadonlyGraph<Q>, ...args: Variables): AsyncIterableIterator<Graph>
}
```

```typescript
export interface Lens<V> extends ReadonlyDataset<Quad> {
  [Symbol.iterator](): Iterator<Quad>
  [Symbol.asyncIterator](): AsyncIterator<[ReadonlyDataset<Quad>, ReadonlyDataset<Quad>]>
  then(resolve: (value: V) => void, reject: (error: unknown) => void): void
}
```


```typescript
export interface LensFunction<V = unknown, Q extends Quad = Quad, Variables extends unknown[]> {
  (this: ReadonlyGraph<Q>, ...args: Variables): Lens<V>
}
```
