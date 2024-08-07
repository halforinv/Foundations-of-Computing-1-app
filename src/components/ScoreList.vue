<script setup lang="ts">
import { ref } from 'vue'

interface Person {
  name: string
  score: number
}

const scores = ref<Person[]>([
])
const newItemName = ref('')
const newScore = ref(0)

const addPerson = () => {
  scores.value.push({ name: newItemName.value, score: newScore.value })
}
</script>

<template>
  <div>
    <ul>
      <li v-for="person in scores" :key="person.name" :class="{ perfect: person.score == 100}">
        <div>名前: {{ person.name }}</div>
        <div>{{ person.score }} 点</div>
        <div v-if="person.score < 60" :key="person.name" :class="{ bad: person.score << 60}">再履修</div>
      </li>
    </ul>
    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      <label>
        点数
        <input v-model="newScore" type="number" />
      </label>
      <button @click="addPerson">追加</button>
    </div>
  </div>
</template>

<style>
.perfect {
  color: blue;
}
.bad {
  color: red;
}
</style>