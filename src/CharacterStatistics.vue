<script>
export default {
  props: {
    characters: {
      type: Array,
      required: true
    }
  },
  computed: {
    characteristicStatistics() {
      const allCharacteristics = this.characters.reduce((acc, character) => {
        return [...new Set(acc.concat(character.characteristics))]
      }, [])

      const statistics = allCharacteristics.reduce((acc, characteristic) => {
        acc[characteristic] = 0
        return acc
      }, {})

      this.characters.forEach((character) => {
        allCharacteristics.forEach((characterType) => {
          if (character.characteristics.includes(characterType)) {
            statistics[characterType]++
          }
        })
      })

      return statistics
    }
  }
}
</script>

<template>
  <h2>Statistics</h2>
  <ul>
    <li v-for="(stat, key) in characteristicStatistics" :key="`char-${stat}-${key}`">
      {{ key }}: {{ stat }}
    </li>
  </ul>
</template>
