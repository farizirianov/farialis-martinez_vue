<template>
  <div>
    <div class="options-container">
      <div class="options-block">
        <h4>Available Options</h4>
        <textarea
          readonly
          rows="10"
          cols="30"
          @click="toggleOption('available', $event)"
        >
          {{ availableOptionsText }}
        </textarea>
      </div>
      <div class="options-block">
        <h4>Disabled Options</h4>
        <textarea
          readonly
          rows="10"
          cols="30"
          @click="toggleOption('disabled', $event)"
        >
          {{ disabledOptionsText }}
        </textarea>
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
    // availableOptions() {
    //   return this.options.options.filter((option) => option.status === 'Available');
    // },
    // disabledOptions() {
    //   return this.options.filter((option) => option.status === 'Disabled');
    // },
    // availableOptionsText() {
    //   return this.availableOptions.map((option) => option.label).join('\n');
    // },
    // disabledOptionsText() {
    //   return this.disabledOptions.map((option) => option.label).join('\n');
    // },
  },
  methods: {
    toggleOption(type, event) {
      const clickedLine = event.target.selectionStart;
      const lines =
        type === 'available'
          ? this.availableOptionsText.split('\n')
          : this.disabledOptionsText.split('\n');
      let charCount = 0;

      for (let i = 0; i < lines.length; i++) {
        charCount += lines[i].length + 1;
        if (clickedLine <= charCount) {
          const optionIndex = this.options.findIndex(
            (option) => option.name === lines[i]
          );
          this.$emit('update-option', optionIndex);
          break;
        }
      }
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
}
textarea {
  width: 100%;
  cursor: pointer;
}
</style>
