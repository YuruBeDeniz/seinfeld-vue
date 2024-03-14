<script>
import CharacterStatistics from './CharacterStatistics.vue'

export default {
  components: {
    CharacterStatistics
  },
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
  <!-- v-bind to make it dynamic -->
  <CharacterStatistics v-bind:characters="characterList" />
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
