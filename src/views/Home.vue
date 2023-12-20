<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="12" sm="8" md="6" class="d-flex flex-column justify-center">
        <v-text-field label="Enter Text" v-model="text" outlined></v-text-field>
        <v-btn color="primary" @click="generateHash">Generate MD5 Hash</v-btn>
        <h1 v-if="hash" class="mt-8 text-center" style="word-wrap: break-word">
          <span class="highlight">{{ hash.substring(0, 12) }}</span
          ><br />{{ hash.substring(12) }}
        </h1>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts" setup>
import md5 from "md5";
import { ref } from "vue";

const text = ref("");
const hash = ref("");

function generateHash() {
  hash.value = md5(text.value);
}
</script>

<style>
.highlight {
  color: red;
  font-weight: bold;
}
</style>
