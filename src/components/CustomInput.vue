<script setup lang="ts">
import { ref, onMounted, watch } from "vue";

const props = defineProps({
  modelValue: {
    type: String,
    default: "",
    required: true,
  },
  disabled: { type: Boolean, default: true },
});

const inputRef = ref<HTMLInputElement>();

const onValueChange = (value: string) => emit("update:modelValue", value);

watch(() => props.modelValue, (newValue, oldValue) => {
  console.log(newValue);
  console.log(oldValue);
})

defineExpose({
  inputRef,
});

const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <input ref="inputRef" class="input" type="text" :value="modelValue" :disabled="disabled" @input="onValueChange($event.target.value)" />
</template>

<style scoped>
input {
  border: none;
}
input:disabled {
  background-color:transparent;
  color: black;
}
</style>
