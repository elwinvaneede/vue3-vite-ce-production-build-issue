<script setup lang="ts">
import { ref } from "vue";

const toggle = ref(true);

class Test extends HTMLElement {
  input: HTMLInputElement;

  constructor() {
    super();

    const shadow = this.attachShadow({ mode: "open" });
    shadow.innerHTML = `<input type="text" />`;
    this.input = shadow.querySelector("input")!;
  }

  set value(val) {
    this.input.value = val;
  }

  get value() {
    return this.input.value;
  }
}

customElements.define("test-component", Test);
</script>

<template>
  <button @click="toggle = !toggle">toggle</button>

  <div v-if="toggle">
    A
    <test-component value="input A"></test-component>
  </div>
  <div v-else>
    B
    <test-component value="input B"></test-component>
  </div>
</template>
