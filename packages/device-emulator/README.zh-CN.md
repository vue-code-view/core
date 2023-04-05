# device-emulator

device-emulator 是一个 Vue 组件，用于在网页中模拟 Chrome 浏览器上的各种设备，例如 iPhone、iPad、Android 设备等。它可以帮助开发人员在实际设备不可用的情况下，快速测试和调试响应式布局、媒体查询等功能。

## 安装

使用 npm 或者 yarn 安装：

```bash
npm install device-emulator --save
# 或者
yarn add device-emulator

```

## 使用

在 Vue 项目中，可以通过 import 导入 device-emulator 组件，然后在模板中使用。例如：

```vue
<template>
  <div>
    <device-emulator :device-type="deviceType">
      <!-- 在这里放置要测试的内容 -->
      <p>Hello, world!</p>
    </device-emulator>
  </div>
</template>

<script>
import DeviceEmulator from 'device-emulator'

export default {
  components: {
    DeviceEmulator
  },
  data () {
    return {
      deviceType: 'iPhone X'
    }
  }
}
</script>
```

在上面的代码中，device-emulator 组件被嵌套在一个 div 元素中，并通过 device-type 属性指定了要模拟的设备类型。在组件的插槽中，可以放置要测试的内容，例如一个段落元素。

## Props

device-emulator 组件支持以下属性：

- device-type：要模拟的设备类型，可选值包括 iPhone X、iPad、Galaxy S5、Pixel 2 等，默认值为 iPhone X。

## 插槽

device-emulator 组件支持一个默认插槽，用于放置要测试的内容。

## 使用场景

快速测试响应式布局、媒体查询等功能。
在不同设备上测试网站的兼容性。

## 示例

上图展示了 device-emulator 组件在模拟 iPhone X 设备时的效果，可以看到页面被缩小，并出现了一个类似 iPhone X 的框架。组件中的内容则按比例缩小，以适应设备的屏幕尺寸。
