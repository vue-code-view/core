# vcv

## refers

<https://pnpm.io/zh/workspaces>
<https://github.com/vueuse/vueuse/blob/main/packages/core/useElementSize/index.ts>
<https://github.com/wheatjs/vue-hako>
<https://www.npmjs.com/package/react-device-emulator>
<https://play.vueuse.org/>
<https://play.tailwindcss.com/>
<https://developer.mozilla.org/zh-CN/docs/Web/API/Resize_Observer_API>
<https://developer.mozilla.org/zh-CN/docs/Web/API/Window/getComputedStyle>

<https://vedanshmehra.hashnode.dev/setting-up-a-monorepo-with-vite-typescript-and-pnpm-workspaces>

## import

```bash
# pnpm-monorepo/packages/device-emulator
pnpm add @vcv/shared
```

## publish

默认情况下，作用域包是私有的。要发布私有模块，您需要是付费的私有模块用户。

公共作用域模块是免费的，不需要付费订阅。若要发布公共作用域模块，请在发布时设置 access 选项。此选项将保留为所有后续发布设置。

```bash
npm publish --access=public
```
