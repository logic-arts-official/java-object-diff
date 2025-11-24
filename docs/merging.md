# Merging Objects

`java-object-diff` not only makes it easy to find differences between objects, it also allows you to merge them, by providing a simple, yet effective assignment mechanism. Every node in the object graph returned by the `ObjectDiffer` provides setter methods, which can be used to change the state of an underlying object instance, as long as it is of the same type as the compared objects.

## Overview

The library provides multiple ways to apply changes:

* **canonicalSet** - Sets a value at the node's location in the object graph
* **canonicalGet** - Reads a value from the node's location
* **canonicalUnset** - Removes/resets a value (nulls objects, removes from collections)

## Basic Merging Example

Here's a simple example of merging changes from a working object into a base object:

```java
// Create objects
Person base = new Person("John", "Doe", 30);
Person working = new Person("John", "Smith", 31);

// Compare
DiffNode diff = ObjectDifferBuilder.buildDefault().compare(working, base);

// Merge changes into base
diff.visit(new DiffNode.Visitor() {
    public void node(DiffNode node, Visit visit) {
        if (node.hasChanges() && !node.hasChildren()) {
            // Apply each leaf change
            node.canonicalSet(base, node.canonicalGet(working));
        }
    }
});

// Now base has been updated with changes from working
```

## Three-Way Merge

For more complex scenarios like resolving concurrent updates:

```java
Person base = loadFromDatabase(id);
Person modified1 = applyUserEdits(base);
Person modified2 = applyOtherUserEdits(base);

// Compare both versions against base
DiffNode diff1 = ObjectDifferBuilder.buildDefault().compare(modified1, base);
DiffNode diff2 = ObjectDifferBuilder.buildDefault().compare(modified2, base);

// Merge non-conflicting changes
Person merged = base.clone();
mergeNonConflicting(merged, diff1, diff2);
```

## Custom Merge Strategies

Since the requirements for a merging mechanism can vary strongly, this library doesn't try to implement every possible approach. Instead, it provides the building blocks to implement your own strategy.

### Example: Selective Property Merge

```java
// Only merge specific properties
Set<String> allowedProperties = Sets.newHashSet("age", "email");

diff.visit(new DiffNode.Visitor() {
    public void node(DiffNode node, Visit visit) {
        if (node.hasChanges() && !node.hasChildren()) {
            String propertyName = node.getPropertyName();
            if (allowedProperties.contains(propertyName)) {
                node.canonicalSet(target, node.canonicalGet(source));
            }
        }
    }
});
```

### Example: Conflict Detection

```java
boolean hasConflicts = false;

diff.visit(new DiffNode.Visitor() {
    public void node(DiffNode node, Visit visit) {
        if (node.getState() == DiffNode.State.CHANGED) {
            Object baseValue = node.canonicalGet(base);
            Object headValue = node.canonicalGet(head);
            Object workingValue = node.canonicalGet(working);
            
            // Check if both modified the same property differently
            if (!Objects.equals(baseValue, headValue) && 
                !Objects.equals(baseValue, workingValue) &&
                !Objects.equals(headValue, workingValue)) {
                hasConflicts = true;
                System.out.println("Conflict at: " + node.getPath());
                visit.stop(); // Stop on first conflict
            }
        }
    }
});
```

## Reference Implementation

For a complete example, see the [ObjectMerger](https://github.com/logic-arts-official/java-object-diff/blob/master/src/main/java/de/danielbechler/diff/ObjectMerger.java) class in the source code.

## Best Practices

1. **Always work on clones** when merging to avoid unintended side effects
2. **Validate changes** before applying them
3. **Handle conflicts explicitly** - don't silently overwrite conflicting changes
4. **Use transactions** when merging database entities
5. **Log merge operations** for audit purposes
6. **Test edge cases** like null values, empty collections, and circular references

## Common Use Cases

* **Database Conflict Resolution** - Merge concurrent updates to the same entity
* **Form Updates** - Apply user-submitted changes to existing objects
* **Data Synchronization** - Sync objects between systems
* **Partial Updates** - Apply only specific field changes
* **Optimistic Locking** - Detect and resolve version conflicts