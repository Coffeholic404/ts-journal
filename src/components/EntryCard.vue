<script lang="ts" setup>
import DateDisplay from "@/components/DataDisplay.vue";
import UseEmojis from "@/composables/UseEmojis";
import type Entry from "@/types/Entry"
import {inject} from "vue"
import { userInjectionKey } from '@/injectKeys'

const { findEmoji } = UseEmojis();
const user = inject(userInjectionKey)

defineProps<{
  entry: Entry;
}>()
</script>
<template>
  <div class="entry-card">
    <div class="entry-card-body">
      <component width="75" :is="findEmoji(entry.emoji)"></component>
      <div class="entry-text">{{ entry.body }}</div>
    </div>
    <div class="entry-footer">
      <DateDisplay :date="entry.createAt" class="mr-2" /> |
      <span class="ml-2">{{ user?.username || "anonymous"}}</span>
    </div>
  </div>
</template>