# Server Component Relocation Guide

## Pattern: Inline or Relocate Single-Use Server Components

When a server component in `src/components/` has exactly one consumer, it's unnecessarily abstracted. Single-use server code is better placed at the consumer site.

## Decision Tree

```
Is the component used in more than one place?
├── YES → Keep as shared component
└── NO → Relocate
    ├── Is it small (<50 lines)? → Inline at consumer
    └── Is it large (50+ lines)? → Move to consumer's _components/
```

## Steps to Relocate

1. **Identify single-use**: Search for imports of the component
2. **Check consumer**: Identify the single page/layout that uses it
3. **Choose destination**:
   - Small: Inline into the consumer file
   - Large: Create `src/app/<route>/_components/<ComponentName>.tsx`
4. **Move the file**: Copy code to new location
5. **Update imports**: Fix the consumer's import path
6. **Delete original**: Remove from `src/components/`
7. **Verify**: Run build and tests

## Example

### Before
```
src/components/ServerDataFetcher.tsx  (used only by app/dashboard/page.tsx)
```

### After
```
src/app/dashboard/_components/ServerDataFetcher.tsx
```

## Benefits
- Reduced cognitive overhead
- Clear ownership (component lives with its consumer)
- Easier to understand component's purpose
- Simpler component directory

## Rubric
This follows the team rubric established for component disposition audits.
