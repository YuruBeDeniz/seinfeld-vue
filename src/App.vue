<script>
export default {
  data: () => ({
    newCharacter: {
      name: '',
      characteristics: []
    },
    characterList: [
      { name: 'George', characteristics: ['Selfish', 'Spineless'] },
      { name: 'Kramer', characteristics: ['Selfish', 'Charismatic', 'Idol'] },
      { name: 'Elaine', characteristics: ['Selfish', 'Idol'] },
      { name: 'Jerry', characteristics: ['Phoney', 'crazy', 'Selfish'] },
      { name: 'Soup Nazi', characteristics: ['Angry'] }
    ],
    favoriteList: []
  }),
  computed: {
    characteristicStatistics() {
      const allCharacteristics = this.characterList.reduce((acc, character) => {
        return [...new Set(acc.concat(character.characteristics))]
      }, [])

      const statistics = allCharacteristics.reduce((acc, characteristic) => {
        acc[characteristic] = 0
        return acc
      }, {})

      this.characterList.forEach((character) => {
        allCharacteristics.forEach((characterType) => {
          if (character.characteristics.includes(characterType)) {
            statistics[characterType]++
          }
        })
      })

      return statistics
    }
  },
  methods: {
    addNewCharacter() {
      this.characterList.push(this.newCharacter)
      this.newCharacter = { name: '' }
    },
    favoriteCharacter(character) {
      if (!this.favoriteList.find((fav) => fav.name === character.name)) {
        this.favoriteList.push(character)
      }
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

  <h1>Seinfeld characters:</h1>
  <p v-if="characterList.length === 0">There are no characters..</p>
  <ul v-else>
    <li v-for="(character, index) in characterList" :key="`even-character-${index}`">
      <p>{{ character.name }}</p>
      <button @click="favoriteCharacter(character)">Add to Favorite</button>
    </li>
  </ul>
  <h2>Favorite Characters</h2>
  <ul v-if="favoriteList.length > 0">
    <li v-for="(favorite, index) in favoriteList" :key="`comma-list-character-${index}`">
      {{ favorite.name }}
    </li>
  </ul>
  <p v-else>No favorite characters yet</p>

  <pre>
      {{ newCharacter }}
    </pre
  >
  <label for="character-name">Name</label>
  <input type="text" v-model="newCharacter.name" @keyup.enter="addNewCharacter" />
</template>
