<script lang="ts" setup>
import EmojiField from '@/components/EmojjiField.vue'
import ArrowCircleRight from '@/assets/icons/arrow-circle-right.svg'
import type Emoji from '@/types/Emoji'
import { ref, computed, onMounted, inject } from 'vue'
import type Entry from '@/types/Entry'
import { userInjectionKey } from '@/injectKeys'
// data
const body = ref('')
const emoji = ref<Emoji | null>(null)
const textCount = computed(() => body.value.length)
const maxChar = 280 as number
const user = inject(userInjectionKey);

//template ref
const textarea =ref<HTMLTextAreaElement | null>(null);
onMounted(() => textarea.value?.focus())

//Events
const emit = defineEmits<{
  (e: '@create', entry: Entry): void
}>()

//methods
const handleTextInput = (e: Event) => {
  e.preventDefault()
  const textarea = e.target as HTMLTextAreaElement
  textarea.value.length <= maxChar
    ? (body.value = textarea.value)
    : (body.value = textarea.value = textarea.value.substring(0, 280))
}
const handleSubmit = () => {
  emit('@create', {
    body: body.value,
    emoji: emoji.value,
    createAt: new Date(),
    userId: 1,
    id: Math.random()
  })
  body.value = ''
  emoji.value = null
}
</script>
<template>
  <form class="entry-form" @submit.prevent="handleSubmit">
    <textarea 
    :value="body" 
    ref="textarea"
    @keyup="handleTextInput" 
    :placeholder="`New Journal Entry for ${user?.username || 'anonymous'}`"></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>{{ textCount }} / {{ maxChar }}</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
