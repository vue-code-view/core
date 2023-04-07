<template>
  <div class="media-query-toolbar">
    <div class="toolbar-header">
      <span>Screen size:</span>
      <button v-for="size in sizes" :key="size.name" :class="{ active: activeSize === size }"
        @click="setActiveSize(size)">
        {{ size.name }}
      </button>
    </div>
    <div class="toolbar-body">
      <label>Custom size:</label>
      <input type="number" v-model.number="customWidth" @change="setCustomSize" /> x
      <input type="number" v-model.number="customHeight" @change="setCustomSize" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sizes: [
        { name: 'Mobile', width: 375, height: 667 },
        { name: 'Tablet', width: 768, height: 1024 },
        { name: 'Laptop', width: 1366, height: 768 },
        { name: 'Desktop', width: 1920, height: 1080 }
      ],
      activeSize: null,
      customWidth: null,
      customHeight: null
    };
  },
  mounted() {
    this.activeSize = this.sizes[0];
    this.$emit('change', this.activeSize);
  },
  methods: {
    setActiveSize(size) {
      this.activeSize = size;
      this.$emit('change', size);
    },
    setCustomSize() {
      const size = { name: `${this.customWidth} x ${this.customHeight}`, width: this.customWidth, height: this.customHeight };
      this.activeSize = size;
      this.$emit('change', size);
    }
  }
};
</script>

<style>
.media-query-toolbar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #fff;
  z-index: 100;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 10px;
  box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.15);
}

.toolbar-header {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}

.toolbar-header button {
  margin: 0 5px;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  background-color: #f5f5f5;
  color: #333;
  cursor: pointer;
}

.toolbar-header button.active {
  background-color: #333;
  color: #fff;
}

.toolbar-body {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}

.toolbar-body input {
  width: 70px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin: 0 5px;
  text-align: center;
}
</style>
