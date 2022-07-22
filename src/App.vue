<script setup lang="ts">
import CustomInput from "@/components/CustomInput.vue";
import { ref, onMounted } from "vue";

const items = ref([
  {
    name: "Anes",
    age: 28,
  },
  {
    name: "Anes2123",
    age: 65,
  },
  {
    name: "Anes2",
    age: 65,
  },
]);

const childRef = ref<InstanceType<typeof CustomInput> | null>(null);
const focusedIdx = ref<number>();

const focusInput = (i: number) => {
  focusedIdx.value === i ? (focusedIdx.value = -1) : (focusedIdx.value = i);
  childRef.value[i].inputRef.disabled = !childRef.value[i].inputRef.disabled;
  childRef.value[i].inputRef.focus();

  if (focusedIdx.value !== i) {
    console.log("Updateovani ref => ", items.value);
  }
};

const testClick = () => {
  items.value.push({ name: "", age: Math.floor(Math.random() * 100) });
};
</script>

<template>
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Age</th>
        <th>Actions</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="(item, i) in items" :key="i">
        <td>
          <CustomInput type="text" ref="childRef" v-model="item.name" />
        </td>

        <td>{{ item.age }}</td>

        <td>
          <button @click="focusInput(i)">
            <span v-if="focusedIdx !== i">Edit</span>
            <span v-else>Save</span>
          </button>
        </td>
      </tr>
    </tbody>

    <button @click="testClick()">Click me</button>
  </table>
</template>

<style scoped>
table,
th,
td {
  border: 1px solid black;
}
</style>
