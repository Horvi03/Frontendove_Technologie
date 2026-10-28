<script setup>
import { ref, watch } from 'vue'
import B from './B.vue'

const number = ref('')
const message = ref('Zatiaľ sa hodnota nezmenila.')
const changeCount = ref(0)

// Zoznam začína aktuálnou hodnotou.
const recentValues = ref([0])

// Poistka, aby oprava hodnoty nespôsobila dvojité započítanie.
let skipCorrectionCallback = false

watch(number, (newValue, oldValue) => {
  // Počas písania samotného znamienka ešte neprepočítavame hodnotu.
  if (newValue === '' || newValue === '-') return

  const numericValue = Number(newValue)

  // Neplatný vstup ignorujeme.
  if (Number.isNaN(numericValue)) return

  const correctedValue = Math.min(100, Math.max(0, numericValue))

  if (correctedValue !== numericValue) {
    number.value = String(correctedValue)
    return
  }

  const previousValue = Number(oldValue)
  if (Number.isNaN(previousValue) || correctedValue === previousValue) return

  message.value = `Hodnota sa zmenila z ${previousValue} na ${correctedValue}.`
  changeCount.value++

  recentValues.value.push(correctedValue)
  if (recentValues.value.length > 5) {
    recentValues.value.shift()
  }
})

</script>

<template>
  <section>
    <h2>Komponent A</h2>

    <label for="number-input">Zadaj číslo od 0 do 100:</label>
    <input
      id="number-input"
      v-model.number="number"
      type="text"
      inputmode="decimal"
    />

    <p>Aktuálna hodnota: {{ number }}</p>
    <p>{{ message }}</p>
    <p>Počet zmien: {{ changeCount }}</p>

    <h3>Posledných päť hodnôt</h3>
    <ol>
      <li v-for="(value, index) in recentValues" :key="index">
        {{ value }}
      </li>
    </ol>

    <!-- Komponent B dostáva hodnotu ako reťazec. -->
    <B :number-as-string="String(number)" />
  </section>
</template>