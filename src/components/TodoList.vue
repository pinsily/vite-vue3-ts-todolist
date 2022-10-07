<template>
  <h1 class="text-3xl mb-4">{{ msg }}</h1>
  <div>
    <input type="text" v-model="newItem" class="pt-1 pb-1 pl-3 pr-3 border-collapse mr-4">
    <button @click="addItem" class="pt-1 pb-1 pl-2 pr-2 bg-blue-800">添加</button>
  </div>
  <div>
    <ul class="list-inside">
      <li v-for="(item, index) in items" :key="item.id" class="list-none mt-2 max-w-md">
        <div class="flex flex-row">
          <div class="w-70 text-left">{{ item.title }}</div>
          <div @click="finishItem(index)" class="text-left">完成</div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">

import { ref } from 'vue';

defineProps<{ msg: string }>();

const newItem = ref<string>("");

interface Item {
  id: number,
  title: string
}

let incrId: number = 0;

const items = ref<Item[]>([]);

function finishItem(index: number): void {
  items.value.splice(index, 1)
}

function addItem(): void {
  if (!newItem.value) {
    return
  }

  const obj: Item = {
    id: incrId,
    title: newItem.value
  };

  items.value.push(obj);

  incrId++;

  newItem.value = "";
}

</script>