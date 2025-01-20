SelectUnselectField.vue
<template>
  <div>
    <div class="options-container">
      <div class="options-block">
        <h4>Available Options</h4>
        <div class="options-list">
          <div
            v-for="option in availableOptions"
            :key="option.id"
            class="option-item"
            @click="toggleOption(option)"
          >
            {{ option.label }}
          </div>
        </div>
      </div>
      <div class="options-block">
        <h4>Disabled Options</h4>
        <div class="options-list">
          <div
            v-for="option in disabledOptions"
            :key="option.id"
            class="option-item"
            @click="toggleOption(option)"
          >
            {{ option.label }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SelectUnselectField',
  props: {
    options: {
      type: Array,
      required: true,
    },
  },
  computed: {
    availableOptions() {
      return this.options.filter((option) => option.status === 'Available');
    },
    disabledOptions() {
      return this.options.filter((option) => option.status === 'Disabled');
    },
  },
  methods: {
    toggleOption(option) {
      option.status = option.status === 'Available' ? 'Disabled' : 'Available';
      this.$emit('update-options', [...this.options]);
    },
  },
};
</script>

<style scoped>
.options-container {
  display: flex;
  justify-content: space-between;
}
.options-block {
  width: 45%;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 2px;
}
.options-list {
  max-height: 200px;
  overflow-y: auto;
  text-underline-offset: 0;
  padding: 5px;
  border-radius: 5px;
}
.option-item {
  padding: 5px;
  cursor: pointer;
}

</style>
