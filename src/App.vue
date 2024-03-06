<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import { reactive } from "vue"
import type User from "./types/User";
import type Entry from "./types/Entry";

const user: User = reactive({
  id:1,
  username:"taqe",
  settings:[],
});

// console.log(user)
const handlCreateEntry = (entry: Entry) => {

}
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
     <EntryEditor @@create="handlCreateEntry"/>
    <ul>
      <li>
        <EntryCard />
      </li>
    </ul> 
  </main>
</template>