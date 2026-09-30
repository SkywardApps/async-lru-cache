# async-lru-cache

A promise-aware LRU cache. `memoizeAsync` caches the promise itself, so concurrent callers share one in-flight call, and a rejected promise is evicted instead of cached.

## Install

```bash
npm install @skywardapps/async-lru-cache
```

## Usage

```ts
import { AsyncLruCache } from '@skywardapps/async-lru-cache';

const cache = new AsyncLruCache<string, User>({ max: 500 });
const getUser = cache.memoizeAsync((id: string) => fetchUser(id));

await getUser('42'); // calls fetchUser
await getUser('42'); // served from the cache
```

The first argument is the cache key by default. Pass a `hashFn` as the second argument to `memoizeAsync` to build the key from all the arguments. Constructor options go straight to [lru-cache](https://www.npmjs.com/package/lru-cache).

Maintained by [Nicholas Elliott](https://nicholasmtelliott.com) ([@NicholasMTElliott](https://github.com/NicholasMTElliott)).
