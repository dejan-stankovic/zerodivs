<template>
  <div class="output-code">
    <codemirror
      v-model="css"
      :options="codeMirrorOptions"
      class="code-editor code-editor-css-output"
    />
    <CopyButton :content="css" class="copy-output-to-clipboard"/>
  </div>
</template>

<script>
import layers2css from "@/common/layers2css";
import store from "@/store";
import { codemirror } from "vue-codemirror-lite";
import CopyButton from "@/components/CopyButton/CopyButton";
require("codemirror/mode/css/css");
require("codemirror/theme/nord.css");
export default {
  components: {
    codemirror,
    CopyButton
  },
  computed: {
    css() {
      return layers2css({ layers: this.shapesLayers });
    },
    codeMirrorOptions() {
      return {
        height: "auto",
        lineWrapping: true,
        mode: "css",
        readOnly: true,
        theme: "nord"
      };
    },
    shapesLayers() {
      return store.getters.allLayers;
    }
  },
  methods: {
    close() {
      this.$router.push({ name: "editor" });
    }
  }
};
</script>

<style scoped>
.css-output {
  position: relative;
}
.code-editor {
  width: 100%;
  font-size: 0.75rem;
}
</style>

<style>
.code-editor-css-output .CodeMirror {
  height: auto;
  padding: 0.5rem 1rem;
}
</style>