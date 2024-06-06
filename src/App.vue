<template>
  <main>
    <div v-if="showModel" class="overlay">
      <div class="model">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"> </textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModel = true">+</button>
      </header>

      <div class="card-container">
        <!-- using directives  -->
        <div
          v-for="note in note"
          :key="note.id"
          class="card"
          :style="{ backgroundColor: note.backgroundColor }"
        >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString('en-UK') }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<!-- script -->
<script setup>
import { ref } from 'vue'

const showModel = ref(false)

const newNote = ref('')

const errorMessage = ref('')

const note = ref([])

function getRandomColor() {
  return 'hsl(' + Math.random() * 360 + ', 100%, 75%)'
}

const addNote = () => {
  if(newNote.value.length < 15) {
    return errorMessage.value = 'Note must be at least 15 characters'
  }
  note.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  })

  showModel.value = false
  newNote.value = ''
  errorMessage.value = ''
}
</script>

<!-- style -->

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 3rem;
}

header button {
  background-color: rgb(21, 20, 20);
  color: white;
  border: none;
  width: 50px;
  padding: 10px;
  height: 50px;
  border-radius: 100%;
  font-size: 20px;
  cursor: pointer;
}
header button:hover {
  background-color: #605e5e;
}

/* .main-text {
  font-size: 1.2rem;
  color: white;
  margin-top: 30px;
} */

.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

.date {
  font-size: 0.8rem;
  color: rgb(21, 20, 20);
  font-weight: bold;
}
.card-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}
.model {
  width: 750px;
  background-color: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  position: relative;
  display: flex;
  flex-direction: column;
}

.model button {
  background-color: rgb(21, 20, 20);
  color: white;
  font-size: 20px;
  border: none;
  padding: 20px;
  width: 100%;
  border-radius: 10px;
  font-size: 20px;
  cursor: pointer;
  margin-top: 15px;
}
.model .close {
  background-color: rgb(203, 12, 12);
  margin-top: 7px;
}
.model p {
  color: red;
  font-size: 1.2rem;
  margin-top: 10px;
}
</style>
