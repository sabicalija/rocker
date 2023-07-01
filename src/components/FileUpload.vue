<template>
  <div>
    <input type="file" @change="onChangeFile" accept=".musicxml" />
    <button @click="onClickUpload">Upload</button>
    <div v-html="svg"></div>
  </div>
</template>

<script setup>
import { ref, version } from "vue";
// import { toolkit } from "verovio";

// import createVerovioModule from "verovio/wasm";
// import { VerovioToolkit } from "verovio/esm";

import verovio from "verovio";

const file = ref(null);
const svg = ref("");

// const tk = new toolkit({
//   pageHeight: 5000,
//   pageWidth: 1000,
//   adjustPageHeight: true,
//   scale: 50,
// });

let tk = null;

// createVerovioModule().then((VerovioModule) => {
//   tk = new VerovioToolkit(VerovioModule);
// });

verovio.module.onRuntimeInitialized = function () {
  tk = new verovio.toolkit();
  tk.setOptions({
    scale: 70,
    landscape: true,
    adjustPageWidth: true,
  });
};

const onChangeFile = (e) => {
  file.value = e.target.files[0];
};

const onClickUpload = () => {
  if (file.value) {
    const reader = new FileReader();
    reader.onload = (e) => {
      if (tk) {
        tk.loadData(e.target.result);
        svg.value = tk.renderToSVG(1, {});
      }
    };
    reader.readAsText(file.value);
  }
};
</script>

<style lang="scss">
// g.staff > *,
// g.barLine > *,
// g.ledgerLines > *,
// g.measure,
// g.label,
// g.grpSym,
// g.section,
// g.pb,
// g.pgHead {
* {
  stroke: white !important;
  fill: white !important;
}
</style>
