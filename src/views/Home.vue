<template>
  <v-container class="mt-16 pt-16">
    <v-row justify="center">
      <v-col cols="12" sm="8" md="6" class="d-flex flex-column justify-center">
        <v-text-field label="Enter Text" v-model="text" outlined></v-text-field>
        <v-switch
          color="primary"
          v-model="uppercase"
          label="Convert to Uppercase"
        ></v-switch>
        <v-btn color="primary" @click="generateHash">Generate MD5 Hash</v-btn>
        <h1 v-if="hash" class="mt-8 text-center" style="word-wrap: break-word">
          <span class="highlight-2">{{ hash.substring(0, 8) }}</span>
          <span class="highlight">{{ hash.substring(8, 12) }}</span
          ><br />{{ hash.substring(12) }}
        </h1>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts" setup>
import md5 from "md5";
import { ref, watch } from "vue";

const text = ref("");
const hash = ref("");
const uppercase = ref(true);

watch(text, (newVal) => {
  if (uppercase.value) {
    text.value = newVal.toUpperCase();
  }
});

function generateHash() {
  hash.value = md5(text.value);
}
</script>

<style>
.highlight-2 {
  color: lawngreen;
  font-weight: bold;
}
.highlight {
  color: red;
  font-weight: bold;
}
</style>
