<template>
  <div>
    <h3>Options</h3>
    <form>
      <input
        type="checkbox"
        name="label"
        id="label"
        v-on:change="handleLabelOption($event.target.checked)"
      />
      <label for="label">Add Label</label>
      <input
        type="text"
        v-if="displayLabel"
        v-model="label"
        v-on:input="addLabelToSchema()"
      />
      <input
        type="checkbox"
        name="placeholder"
        id="placeholder"
        v-on:change="handlePlaceholderOption($event.target.checked)"
      />
      <label for="placeholder">Add Placeholder</label>
      <input
        type="text"
        v-if="displayPlaceholder"
        v-model="placeholder"
        v-on:input="addPlaceholderToSchema()"
      />
    </form>
  </div>
</template>

<script>
export default {
  name: "RenderingCore",
  model: {
    prop: "options",
    event: "update-schema-options"
  },
  props: {
    schema: {
      type: Object
    }
  },
  data: function() {
    return {
      displayLabel: false,
      label: "",
      displayPlaceholder: false,
      placeholder: ""
    };
  },
  methods: {
    handleLabelOption: function(checked) {
      this.displayLabel = checked;
      if (!checked) {
        this.label = "";
        this.$emit("remove-schema-options", "id");
        this.$emit("remove-schema-options", "name");
        this.$emit("remove-schema-options", "label");
      }
    },
    addLabelToSchema: function() {
      if (this.displayLabel) {
        this.$emit("update-schema-options", {
          ...this.schema.options,
          id: this.label.toLowerCase().trim(),
          name: this.label.toLowerCase().trim(),
          label: this.label
        });
      }
    },
    handlePlaceholderOption: function(checked) {
      this.displayPlaceholder = checked;
      if (!checked) {
        this.placeholder = "";
        this.$emit("remove-schema-options", "placeholder");
      }
    },
    addPlaceholderToSchema: function() {
      if (this.displayPlaceholder) {
        this.$emit("update-schema-options", {
          ...this.schema.options,
          placeholder: this.placeholder
        });
      }
    }
  }
};
</script>

<style scoped></style>
