# JS Cache Management

Small JavaScript cache management utility built around a few lightweight classes.

This repository contains a university class project from `2011-10-26`, based on the last commit currently in the git history.

## What It Does

- Creates stable cache keys from input strings using SHA-1.
- Stores generated objects in an in-memory cache.
- Reuses cached objects when the same key is requested again.
- Delegates object creation to a user-provided callback.

## Main Pieces

- `ObjectKey` keeps both the original identifier and its SHA-1 hash.
- `ObjectCreator` wraps the callback used to build fresh objects.
- `Cache` stores objects by hashed key.
- `CacheManager` coordinates cache lookup and object creation.

## Code Layout

- `lib/cache.management.js` contains the main cache management classes and an embedded SHA-1 helper.
- `etc/sha1.js` contains a standalone SHA-1 implementation.

## Example

```js
var manager = new CacheManager(function(objKey, cache) {
  var value = "generated for " + objKey.getIdOriginal();
  cache.addObject(objKey, value);
  return value;
});

manager.fetchObject("user:1");
manager.fetchObject("user:1");
```

On the first call, the callback creates and stores the value. On later calls with the same input, the cached value is returned.
