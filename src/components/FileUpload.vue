<template>
  <div>
    <input type="file" @change="onChangeFile" accept=".musicxml" />
    <button @click="onClickUpload">Upload</button>
    <div ref="renderer"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { OpenSheetMusicDisplay } from "opensheetmusicdisplay";

const file = ref(null);
const renderer = ref(null);

let osmd = null;

onMounted(() => {
  osmd = new OpenSheetMusicDisplay(renderer.value);
  osmd.setOptions({
    backend: "svg",
    drawTitle: true,
    drawLyrics: true,
    autoResize: true,
  });
});

const onChangeFile = (e) => {
  file.value = e.target.files[0];
};

const onClickUpload = () => {
  if (file.value) {
    const reader = new FileReader();
    reader.onload = (e) => {
      osmd.load(e.target.result);
      osmd.render();
    };
    reader.readAsText(file.value);
  }
};
</script>

<style lang="scss"></style>
