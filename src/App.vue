<script>
import CharacterStatistics from './CharacterStatistics.vue'
import CharacterCard from './CharacterCard.vue'
import BaseLayout from './BaseLayout.vue'

export default {
  components: {
    CharacterStatistics,
    CharacterCard,
    BaseLayout
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
    addFavoriteCharacter(payload) {
      console.log(payload)
      if (!this.favoriteList.find((fav) => fav.name === payload.name)) {
        this.favoriteList.push(payload)
      }
    }
  }
}
</script>

<template>
  <BaseLayout>
    <template v-slot:two>
      <h2>Add New Character</h2>
      <pre>
      {{ newCharacter }}
    </pre
      >
      <label for="character-name">Name</label>
      <input type="text" v-model="newCharacter.name" @keyup.enter="addNewCharacter" />
    </template>
  </BaseLayout>
  <!-- v-bind to make it dynamic -->
  <CharacterStatistics v-bind:characters="characterList" />
  <h1>Seinfeld characters:</h1>
  <p v-if="characterList.length === 0">There are no characters..</p>
  <ul v-else>
    <li v-for="(character, index) in characterList" :key="`even-character-${index}`">
      <CharacterCard :character="character" @favorite="addFavoriteCharacter" />
    </li>
  </ul>
  <h2>Favorite Characters</h2>
  <ul v-if="favoriteList.length > 0">
    <li v-for="(favorite, index) in favoriteList" :key="`comma-list-character-${index}`">
      {{ favorite.name }}
    </li>
  </ul>
  <p v-else>No favorite characters yet</p>
</template>
