<template>
  <div>
    <input type="file" @change="onChangeFile" accept=".musicxml" />
    <button @click="onClickUpload">Upload</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
</script>

<style lang="scss"></style>
