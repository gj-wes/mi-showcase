<script setup>
import PreviewCard from '@/components/PreviewCard.vue'
import data from './data.json'
</script>

<template>
  <aside>
    <div class="sticky-container">
      <h1>
        MI Showcase
      </h1>
      <p>
        Examples of how we've used Movable Ink dynamic content in our marketing emails. 
        <br><br>
        Click a preview for more details.
      </p>
      <p>
        If you'd like to know more about any of the Movable Ink functionality please speak to <span>Dipal Patel</span> and <span>Gary Wesolowski</span> in the Email Dev team.
      </p>
    </div>
  </aside>
  <main>
    <PreviewCard v-for="email, i in data.emails" :key="i" :tags="email.tags" :details="email">
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
    color: hsl(var(--pink));
  }
}
.sticky-container {
  position: sticky;
  top: 1rem;
  height: 100%;
  display: flex;
  flex-direction: column;

  :last-child {
    margin-block-start: auto;
  }
}

h1 {
  color: hsl(var(--pink));
  font-size: 1.75rem;
  margin-block-end: 1rem;
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
