# TypeScript

## tsconfig flags that earn their keep

```json
{
  "strict": true,
  "noUncheckedIndexedAccess": true,
  "verbatimModuleSyntax": true
}
```

`noUncheckedIndexedAccess` makes `arr[0]` return `T | undefined` — catches a real class of bugs.
`verbatimModuleSyntax` forces `import type` where it belongs, so bundlers can drop unused imports.

## Types from values

```ts
const ROLES = ["admin", "user"] as const;
type Role = typeof ROLES[number];        // "admin" | "user"

const config = { port: 3000, host: "localhost" } satisfies Record<string, string | number>;
// validated, but port stays `number` instead of widening to `string | number`
```

Prefer a union of literals over `enum` — enums emit runtime code and surprise people on import.

## Exhaustive switch

```ts
function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle": return Math.PI * shape.r ** 2;
    case "square": return shape.side ** 2;
    default: {
      const _never: never = shape; // compile error when a variant is added
      return _never;
    }
  }
}
```

## Gotchas

- `Object.keys(obj)` returns `string[]`; `keyof typeof obj` is the narrow type — cast once at the boundary, not everywhere.
- `as` silences the compiler; `satisfies` checks without changing the inferred type. Reach for `satisfies` first.
- `readonly T[]` and `ReadonlyArray<T>` are the same thing; `as const` on an array gives you a readonly tuple.
- Optional `foo?: T` and `foo: T | undefined` differ under `exactOptionalPropertyTypes`.
