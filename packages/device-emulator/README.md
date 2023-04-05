# device-emulator

## Overview

The Device Emulator Vue Component is a Vue component that simulates a mobile device screen within a desktop browser. This component can be used to test responsive web design and to see how a website or web application looks on different devices.

The Device Emulator Vue Component is designed to be easily customizable and supports various devices and orientations.

## Introduction

Device-Emulator is a Vue component that provides a simulation of different mobile and tablet devices to preview a website's responsiveness and layout. It's inspired by the Chrome DevTools Device Mode.

## Features

- Support for various devices, including iPhones, iPads, Samsung Galaxy, and more.
- Preview website responsiveness and layout.
- Switch between portrait and landscape modes.
- Change the device's scale and resolution.
- Toggle the device's borders and shadow.
- Cross-browser compatibility.

## Installation

To install the Device Emulator Vue Component, simply run:

```bash
npm install device-emulator --save
# 或者
yarn add device-emulator

```

## Usage

To use the Device Emulator Vue Component, first import it into your Vue component:

```javascript
import DeviceEmulator from 'device-emulator-vue'
```

Then, simply add the DeviceEmulator component to your template, passing in the device type and orientation as props:

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
  data() {
    return {
      deviceType: 'iPhone X'
    }
  }
}
</script>
```

## Props

The following props are available for the DeviceEmulator component:

- device: The device type to emulate. Possible values are iphone-5, iphone-6, iphone-6-plus, iphone-x, ipad, ipad-pro, galaxy-s5, pixel-2, pixel-2-xl, and custom (default: iphone-x).
- orientation: The orientation of the device. Possible values are portrait and landscape (default: portrait).
- width: The width of the device in pixels (only applicable if device="custom").
- height: The height of the device in pixels (only applicable if device="custom").

## Props1

- device (String, Required): The device to simulate. Available devices are listed in the table below.
- scale (Number, Optional): The device's scale. Default is 1.
- shadow (Boolean, Optional): Toggle the device's shadow. Default is true.
- border (Boolean, Optional): Toggle the device's border. Default is true.

## Examples

Here are some examples of how to use the Device Emulator Vue Component:

```html
<template>
  <div>
    <!-- iPhone X, portrait -->
    <DeviceEmulator device="iphone-x" orientation="portrait">
      <!-- Your website or application content here -->
    </DeviceEmulator>

    <!-- iPad Pro, landscape -->
    <DeviceEmulator device="ipad-pro" orientation="landscape">
      <!-- Your website or application content here -->
    </DeviceEmulator>

    <!-- Custom device, 800x600, portrait -->
    <DeviceEmulator
      device="custom"
      orientation="portrait"
      :width="800"
      :height="600"
    >
      <!-- Your website or application content here -->
    </DeviceEmulator>
  </div>
</template>

<script>
  import DeviceEmulator from 'device-emulator-vue'

  export default {
    components: {
      DeviceEmulator
    }
  }
</script>
```

## Available Devices

TODO

## License

The Device Emulator Vue Component is open source software licensed under the MIT License.
