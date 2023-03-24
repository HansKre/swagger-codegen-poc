<script setup lang="ts">
import { PetApi, type Pet } from './api-client/ts'
import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <!-- <TheWelcome /> -->
    <div v-for="job in jobs" :key="job.id" class="">
      <h2>{{ job.title }}</h2>
      <p>{{ job.details }}</p>
    </div>
    <div v-if="petM !== undefined">
      <h2>Old Fetch</h2>
      <h3>{{ petM.name }}</h3>
      <p>{{ petM.status }}</p>
    </div>
    <div v-if="petAuto !== undefined">
      <h2>Fetch with Auto-Gen Client</h2>
      <h3>{{ petAuto.name }}</h3>
      <p>{{ petAuto.status }}</p>
      <p>{{ petAuto.photoUrls }}</p>
      <p>{{ petAuto.tags }}</p>
    </div>
  </main>
</template>

<!-- https://upmostly.com/vue-js/get-data-from-an-api-in-a-vue-component-with-the-fetch-api -->
<script lang="ts">
type Job = {
  id: number
  title: string
  details: string
}

type PetManual = {
  name: string
  status: string
}

export default {
  data(): { jobs: Job[]; petM: PetManual | undefined; petAuto: Pet | undefined } {
    return {
      jobs: [
        { title: 'abc', id: 1, details: 'details 1' },
        { title: 'efg', id: 2, details: 'details 2' },
        { title: 'hij', id: 3, details: 'details 3' }
      ],
      petM: undefined,
      petAuto: undefined
    }
  },
  methods: {
    async getPet(id: number) {
      const res = await fetch(`https://petstore.swagger.io/v2/pet/${id}`)
      const pet = await res.json()
      this.petM = pet as PetManual
    },
    async getPetClient(id: number) {
      const client = new PetApi()
      const pet = await client.getPetById(id)
      this.petAuto = pet
    }
  },
  mounted() {
    this.getPet(1)
    this.getPetClient(1)
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
