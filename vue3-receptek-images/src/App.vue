<template>
  <h1>Magyar receptek</h1>
  <div v-if='loading'>Betöltés...</div>
  <div v-else-if='error' style='color:red;'>{{ error }}</div>

  <div class='grid'>
    <RecipeCard v-for='r in receptek' :key='r.id' :recept='r' @details='openDetails'/>
  </div>

  <!-- MODAL (kép + adatok egymás mellett) -->
<div v-if="selected" class="modal-bg" @click.self="selected = null">
  <div class="modal">
    
    <div class="details-container">
      
      <!-- BAL OLDALT A KÉP -->
      <img class="details-img" :src="selected.kep" :alt="selected.nev" />

      <!-- JOBB OLDALT A RÉSZLETEK -->
      <div class="details-card">
        <h2>{{ selected.nev }}</h2>
        <p><strong>Kategória:</strong> {{ selected.kategoria }}</p>
        <p><strong>Leírás:</strong> {{ selected.leiras }}</p>
        <p><strong>Pont:</strong> {{ selected.pont }}/10</p>
        <button class="button" @click="selected = null">Bezárás</button>
      </div>

    </div>

  </div>
</div>

</template>

<script setup>
import { ref, onMounted } from 'vue'
import RecipeCard from './components/RecipeCard.vue'

const receptek = ref([])
const loading = ref(true)
const error = ref('')
const selected = ref(null)

const openDetails = r => selected.value = r

onMounted(async () => {
  loading.value = true
  try {
    const res = await fetch('/data.json')
    if (!res.ok) throw new Error('Hiba a data.json betöltésekor')
    const json = await res.json()
    receptek.value = json.receptek
  } catch(e) {
    error.value = e.message
  } finally {
    loading.value = false
  }
})
</script>
