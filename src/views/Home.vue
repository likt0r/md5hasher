<template>
  <v-container class="mt-10 pt-10">
    <v-row justify="center">
      <v-col cols="12" sm="8" md="6" class="d-flex flex-column justify-center">
        <v-form ref="form" v-model="valid">
          <v-text-field
            label="Enter MAC Address Segment"
            v-model="text"
            :rules="macRules"
            outlined
            clearable
          ></v-text-field>

          <v-btn color="primary" :disabled="!valid" @click="generateHash"
            >Generate MD5 Hash</v-btn
          >
          <h1
            v-if="hash"
            class="mt-8 text-center"
            style="word-wrap: break-word"
          >
            <span class="highlight-2">{{ hash.substring(0, 8) }}</span>
            <span class="highlight">{{ hash.substring(8, 12) }}</span
            ><br />{{ hash.substring(12) }}
          </h1>
          <v-switch
            color="primary"
            v-model="uppercaseInput"
            label="Convert Input to UppercaseInput"
          ></v-switch>
          <v-switch
            color="primary"
            v-model="uppercaseOutput"
            label="Convert Output UppercaseInput"
          ></v-switch>
          <v-switch
            color="primary"
            v-model="macFormedInput"
            label="Input is a MAC-Address (XXYYXXYYXXYY)"
          ></v-switch>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts" setup>
import md5 from "md5";
import { ref, computed, watch } from "vue";

const text = ref("");
const hash = ref("");
const valid = ref(false);
const uppercaseInput = ref(true);
const uppercaseOutput = ref(true);
const macFormedInput = ref(true);

const form = ref(null);

watch(text, (newVal) => {
  if (uppercaseInput.value) {
    text.value = newVal.toUpperCase();
  }
});

const macRules = [
  (v: string) => !!v || "Input is required",
  (v: string) =>
    /^[0-9A-F]{12}$/.test(v) ||
    !macFormedInput.value ||
    "Must be 6 characters, only numbers and A-F",
];

function generateHash() {
  if (valid.value) {
    hash.value = md5(text.value);
  }
  if (uppercaseOutput.value) {
    hash.value = hash.value.toUpperCase();
  }
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
