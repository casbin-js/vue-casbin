# vue-casbin

This package allows you to integrate [Casbin](https://github.com/casbin/node-casbin) (An authorization library) with
your Vue 3 application.

## Installation

```bash
npm install vue-casbin
# or
yarn add vue-casbin
# or
pnpm add vue-casbin
```

## Getting started

This package provides a Vue plugin, several hooks for
new [Vue Composition API](https://v3.vuejs.org/guide/composition-api-introduction.html)

### The plugin

```typescript
import { createApp } from 'vue';
import CasbinPlugin from 'vue-casbin';
import { newEnforcer } from 'casbin';

const enforcer = newEnforcer('model string', 'policy string');

createApp()
  .use(CasbinPlugin, enforcer, {
    useGlobalProperties: true
  }).mount('#app');
```

After that, you can use `$enforcer` and `$enforceSync` in every component.

```vue

<template>
  <p
    v-if='$enforceSync("alice","read","post")'
  >
    Post content.
  </p>
</template>
```

By default, `useGlobalProperties` will mount `$enforcer` and `$enforce` on every component. You can also
use [provide/inject API](https://v3.vuejs.org/guide/component-provide-inject.html) in Vue 3 to get the `enforcer`.

```typescript
createApp()
  .use(CasbinPlugin, enforcer)
  .mount('#app');
```

And inject it with `ENFORCER_KEY`

```vue

<template>
  <p v-if="$whatyouwant.enforceSync('alice', 'read', 'Post')">
    Post content.
  </p>
</template>

<script>
import { ENFORCER_KEY } from 'vue-casbin';

export default {
  inject: {
    $whatyouwant: { from: ENFORCER_KEY }
  }
}
</script>
```

You can also use `useEnforcer` function.

```vue

<template>
  <p v-if="whatyouwant.enforceSync('read', 'Post')">
    Post content.
  </p>
</template>

<script>
import { useEnforcer } from 'vue-casbin';

export default {
  setup() {
    const { whatyouwant } = useEnforcer();
    return {
      whatyouwant
    };
  }
}
</script>
```

## License

This project is licensed under the [Apache 2.0 license](LICENSE).

## Contact

If you have any issues or feature requests, please contact us. PR is welcomed.

- https://github.com/casbin-js/vue-casbin/issues
- zxilly@outlook.com
- Tencent QQ
  group: [546057381](//shang.qq.com/wpa/qunwpa?idkey=8ac8b91fc97ace3d383d0035f7aa06f7d670fd8e8d4837347354a31c18fac885)
