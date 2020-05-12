<template>
  <div id="app">
    <layout>
      <template v-slot:left-content>
        <p>Components</p>
        <draggable v-model="components" v-bind="draggableOptions.components">
          <p v-for="component of components" v-bind:key="component.id">
            {{ component.type }}
          </p>
        </draggable>
      </template>
      <template v-slot:middle-content>
        <h3>Schema</h3>
        <draggable
          v-model="schemas"
          v-bind="draggableOptions.schemas"
          class="dropzone"
        >
          Drop items here
        </draggable>
        <template v-for="schema of schemas">
          {{ schema }}
          <rendering-core
            v-bind:schema="schema"
            v-bind:key="schema.id"
            v-model="schema.options"
            v-on:remove-schema-options="$delete(schema.options, $event)"
          ></rendering-core>
        </template>
      </template>
      <template v-slot:right-content>
        <h3>Preview</h3>
        <template v-for="schema of schemas">
          <div v-bind:key="schema.id">
            <label v-bind:for="schema.options.id"
              >{{ schema.options.label }}
            </label>
            <input v-bind:type="schema.type" v-bind="schema.options" />
          </div>
        </template>
      </template>
    </layout>
  </div>
</template>
<script>
import draggable from "vuedraggable";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "App",
  components: {
    Layout: () => import("./Components/Layout.vue"),
    RenderingCore: () => import("./Components/Rendering/RenderingCore.vue"),
    draggable
  },
  data: function() {
    return {
      draggableOptions: {
        components: {
          group: { name: "components", pull: "clone", put: false }
        },
        schemas: {
          group: { name: "schemas", put: true },
          ghostClass: "ghost-hidden"
        }
      },
      components: [
        {
          id: uuidv4(),
          type: "text",
          options: {
            value: ""
          }
        }
      ],
      schemas: []
    };
  },
};
</script>

<style lang="scss">
body {
  background-color: #283149;
  color: #dbedf3;
  font-family: "Courier New", Courier, monospace;
}

input[type="text"] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  background-color:#404b69;
  color: white;
}

.dropzone {
  height: 140px;
  width: auto;
  border-style: dotted;
  border-color: black;
  text-align: center;
  vertical-align: middle;
  line-height: 140px;
}

.ghost-hidden {
  visibility: hidden;
}
</style>
