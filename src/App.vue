<script setup>
import { computed, ref } from 'vue';
import PreviewCard from '@/components/PreviewCard.vue'
import data from './data.json'

const selectedTags = ref([])

function toggleFilterSelect(tag) {
  if (selectedTags.value.includes(tag)) {
    selectedTags.value = selectedTags.value.filter(t => t !== tag);
  } else {
    selectedTags.value.push(tag)
  }
  
}

const filterPreviews = computed(() => {
  let filtered = data.emails;
  if (selectedTags.value.length !== 0) {
    filtered = data.emails.filter(email => {
      return email.tags.every(tag => { 
        console.log(email.tags, tag, email.tags.every(tag => selectedTags.value.includes(tag)))
        return selectedTags.value.includes(tag)
      })
    })
  }
  return filtered;
})
</script>

<template>
  <aside>
    <div class="sticky-container">
      <h1>
        MI Showcase
      </h1>
      <p>
        If you'd like to know more about any of the Movable Ink functionality please speak to <span>Dipal Patel</span> and <span>Gary Wesolowski</span> in the Email Dev team.
      </p>
    </div>
  </aside>
  <main>
    <PreviewCard v-for="email, i in filterPreviews" :key="i" :tags="email.tags" :details="email">
      <img :src="email.url" :style="{ 'object-position': `${email.offset}` }">
    </PreviewCard>
  </main>
</template>

<style scoped>
:global(*) {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
:global(body) {
  --pink: 332, 78%, 50%;

  font-family: 'Sky Text', sans-serif;
  font-size: 1rem;
  line-height: 1.4;
  background-color: whitesmoke;
}
:global(#app) {
  min-height: 100vh;
  display: grid;
  grid-template-columns: minmax(200px, 15%) 1fr;
}
:global(img) {
  display: block;
  max-width: 100%;
}

aside {
  box-shadow: 0 2px 10px 10px hsla(0, 0%, 50%, 0.2);
  padding: 1rem;

  & p span {
    font-weight: bold;
    color: hsl(332, 78%, 50%);
  }
}
.sticky-container {
  position: sticky;
  top: 1rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h1 {
  color: hsl(var(--pink));
  font-size: 1.75rem;
}

main {
  height: 100vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 2rem;
  padding: 2rem;
  overflow-y: scroll;

  & > :deep(.card) {
    flex: 0 1 150px
  }
}
</style>
