<script setup>
import AddToCal from '@/components/BlockDescriptions/AddToCal.md'
import APIData from '@/components/BlockDescriptions/APIData.md'
import BarChart from '@/components/BlockDescriptions/BarChart.md'
import DynamicImage from '@/components/BlockDescriptions/DynamicImage.md'
import ScratchCard from '@/components/BlockDescriptions/ScratchCard.md'
import Timer from '@/components/BlockDescriptions/Timer.md'
import Weather from '@/components/BlockDescriptions/Weather.md'
defineProps({
  details: Object
})

const model = defineModel({ type: Boolean })

function toggleModel () {
  model.value = !model.value
}
</script>

<template>
  <div class="detail-backdrop"  @click.self="toggleModel">
    <div class="details">
      <div class="close" @click="toggleModel">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M6.4 19L5 17.6l5.6-5.6L5 6.4L6.4 5l5.6 5.6L17.6 5L19 6.4L13.4 12l5.6 5.6l-1.4 1.4l-5.6-5.6z"/></svg>
      </div>
      <div class="img-scroll">
        <img :src="details.url" alt="">
      </div>
      <div class="content">

        <AddToCal     v-if="details?.tags.includes('addtocal')" />
        <APIData      v-if="details?.tags.includes('api')"      />
        <BarChart     v-if="details?.tags.includes('bar')"      />
        <DynamicImage v-if="details?.tags.includes('imgpers')"  />
        <ScratchCard  v-if="details?.tags.includes('scratch')"  />
        <Timer        v-if="details?.tags.includes('timer')"    />
        <Weather      v-if="details?.tags.includes('weather')"  />

        <template v-if="details?.example">
          <h2>
            In this example:
          </h2>
          <p v-html="details.example"></p>
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
.detail-backdrop {
  position: absolute;
  inset: 0;
  background-color: hsla(var(--pink), 0.4);
  display: flex;
  justify-content: center;
  padding: 1rem;
  overflow: hidden;
}
.details {
  padding: 1rem;
  width: 70%;
  background-color: hsl(0, 100%, 100%);
  border-radius: 10px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  position: relative;
}
.close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  cursor: pointer;
  transition: color 0.3s linear;
  &:hover {
    :deep(path) {
      color: #e31c79;
    }
  }
}
.img-scroll {
  overflow-y: scroll;
  border: 2px solid whitesmoke;
}
.content {
  overflow-y: scroll;

  & :deep(h2) {
    color: hsl(var(--pink));
    font-size: 1.5rem;
    margin-block-end: .5rem;
  }
  & :deep(p) {
    font-size: 1.125rem;
  }
}

.block-description {
  margin-block-end: 2rem;

  & :deep(p + p) {
    margin-block-start: 1rem;
  }
}
</style>