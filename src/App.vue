<script setup>
import { ref } from "vue";

const display = ref("");
const buttons = [
  { value: "AC", type: "clear" },
  { value: "DEL", type: "delete" },
  { value: ".", type: "operator" },
  { value: "/", type: "operator" },

  { value: "7" },
  { value: "8" },
  { value: "9" },
  { value: "*", type: "operator" },

  { value: "4" },
  { value: "5" },
  { value: "6" },
  { value: "-", type: "operator" },

  { value: "1" },
  { value: "2" },
  { value: "3" },
  { value: "+", type: "operator" },

  { value: "000" },
  { value: "00" },
  { value: "0" },
  { value: "=", type: "operequalsator" },
];

const update = (btnValue) => {
  display.value = String(display.value);
  if (btnValue === "AC") {
    return (display.value = "");
  }

  if (btnValue === "DEL") {
    return (display.value = display.value.slice(0, -1));
  }

  if (btnValue === "=") {
    return (display.value = eval(display.value));
  }

  if (
    btnValue === "*" ||
    btnValue === "." ||
    btnValue === "+" ||
    btnValue === "-" ||
    btnValue === "/"
  ) {
    if (
      display.value.substr(display.value.length - 1) === "*" ||
      display.value.substr(display.value.length - 1) === "." ||
      display.value.substr(display.value.length - 1) === "+" ||
      display.value.substr(display.value.length - 1) === "-" ||
      display.value.substr(display.value.length - 1) === "/"
    ) {
      return;
    }
    if (display.value === "") {
      return;
    }
  }
  if (
    btnValue === "." &&
    display.value
      .split(/[*|/|-|+]/)
      .pop()
      .includes(".")
  ) {
    return;
  }

  display.value += btnValue;
};
</script>

<template>
  <div class="calculator">
    <input type="text" v-model="display" class="display" disabled />

    <div class="buttons">
      <button
        v-for="btn in buttons"
        :key="btn.value"
        @click="update(btn.value)"
        :class="`button button_${btn.type || 'default'}`"
      >
        {{ btn.value }}
      </button>
    </div>
  </div>
</template>

<style scoped></style>
