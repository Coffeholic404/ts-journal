<script lang="ts" setup>
import EmojiField from "@/components/EmojjiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import type Emoji from "@/types/Emoji";
import { ref, computed} from "vue";

const text = ref("")
const emoji = ref<Emoji | null>(null)
const textCount = computed(()=> text.value.length)
const maxChar = 280 as number;
const handleTextInput = (e: Event) =>{
  e.preventDefault()
  const textarea = e.target as HTMLTextAreaElement;
  (textarea.value.length <= maxChar) ? text.value = textarea.value : text.value = textarea.value = textarea.value.substring(0, 280);
}
</script>
<template>
  <form class="entry-form" @submit.prevent>
    <textarea
    :value="text" 
    @keyup="handleTextInput" 
    placeholder="New Journal Entry"></textarea>
    <EmojiField v-model="emoji"/>
    <div class="entry-form-footer">
      <span>{{ textCount }} / {{ maxChar }}</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
