<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import { ref, reactive } from "vue"
import type User from "./types/User";
import type Entry from "./types/Entry";

const user: User = reactive({
  id:1,
  username:"taqe",
  settings:[],
});

// console.log(user)
const entryArr: Entry[] = reactive([]);
const handlCreateEntry = (entry: Entry) => {
  entryArr.unshift(entry)
  return entryArr
}
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
     <EntryEditor @@create="handlCreateEntry"/>
    <ul>
      <li v-for="entry in entryArr" :key="entry.id">
        <EntryCard :entry="entry"/>
      </li>
    </ul> 
  </main>
</template>