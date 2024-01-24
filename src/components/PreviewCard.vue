<script setup>
import { computed, ref } from 'vue';
import DetailsModal from '@/components/DetailsModal.vue'

const props = defineProps({
  tags: Array,
  details: Object
})

const tagsOutput = computed(() => {

  return props.tags.map(t => {
    const displayText = {
      'api': "API Data",
      'addtocal': "Add to Calendar",
      'bar': "Bar Chart",
      'timer': "Countdown",
      'imgpers': "Dynamic Image",
      'scratch': "Scratch Card",
      'weather': "Weather",
    }

    return displayText[t]
  })

})

const detailShow = ref(false)
</script>

<template>
  <div class="card" @click="detailShow = !detailShow">
    <div class="img-crop">
      <slot />
    </div>
    <div class="tag-container">
      <span v-for="tag, i in tagsOutput" :key="i" class="tag">{{ tag }}</span>
    </div>
  </div>

  <Teleport to="body">
    <Transition>
      <DetailsModal :details="details" v-if="detailShow" v-model="detailShow" />
    </Transition>
  </Teleport>
</template>

<style scoped>
.card {
  border-radius: 5px;
  box-shadow: 2px 0 10px 5px hsla(0, 0%, 50%, 0.2);
  background-color: hsl(0, 100%, 100%);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: box-shadow .3s linear;
  cursor: pointer;

  &:hover {
    box-shadow: 2px 0 10px 5px hsla(var(--pink), 0.2);
  }
}
.img-crop {
  max-height: 200px;
  overflow: hidden;
}
.tag-container {
  padding: .25rem;
  padding-block-end: .125rem;
}
.tag {
  display: inline-block;
  margin-inline-end: .125rem;
  margin-block-end: .125rem;
  background-color: hsl(var(--pink));
  padding: 1px 4px;
  border-radius: 3px;
  white-space: nowrap;
  color: #ffffff;
}
.v-enter-active,
.v-leave-active {
  transition: opacity 0.2s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>