# Device-Emulator

## Overview

## Introduction

Device-Emulator is a Vue component that provides a simulation of different mobile and tablet devices to preview a website's responsiveness and layout. This component can be used to test responsive web design and to see how a website or web application looks on different devices.

It's inspired by the Chrome DevTools Device Mode.

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
npm install @vcv/device-emulator
# or
yarn add @vcv/device-emulator
# or
pnpm add @vcv/device-emulator
```

## Usage

To use the Device Emulator Vue Component, first import it into your Vue component:

```javascript
import { DeviceEmulator } from '@vcv/device-emulator'
import '@vcv/device-emulator/style.css'
```

Then, simply add the DeviceEmulator component to your template, passing in the device type and orientation as props:

```html
<script setup lang="ts">
import { ref } from 'vue'
import { DeviceEmulator } from '@vcv/device-emulator'
import '@vcv/device-emulator/style.css'

const disableScaling = ref(false)
const width = ref(335)
const height = ref(667)
</script>

<template>
  <DeviceEmulator
    class="device-emulator"
    :width="width"
    :height="height"
    :disable-scaling="disableScaling"
  >
    <!-- Your content here -->
  </DeviceEmulator>
</template>
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

## License

Device Emulator is licensed under the terms of the [MIT License](./LICENSE).

Copyright (c) 2023-present Andurils
