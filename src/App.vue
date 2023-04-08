<script setup>
import { ref, reactive } from "vue"
// data 
const overlay = ref(false)

const noteText = ref("")

const noteList = reactive([
  {
    id: Math.floor(Math.random() * 1000000),
    text: "Hello World!!! Vue is taking over",
    date: new Date().toLocaleDateString(),
    backgroundColor: ""
  },
])

const errorMessage = ref("")

// methods
const showOverlay = () => {
  overlay.value = true
}

const hideOverlay = () => {
  overlay.value = false
}

const getRandomColor = () => {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)"
}

const addNewNote = () => {
  if (noteText.value < 9) {
    return errorMessage.value = "note should have 9 or more characters"
  }
  const newNote = {
    id: Math.floor(Math.random() * 1000000),
    text: noteText.value,
    date: new Date().toLocaleDateString(),
    backgroundColor: getRandomColor()
  }
  noteList.push(newNote)
  noteText.value = ""
  errorMessage.value = ""
  hideOverlay()
}

</script>
<template>
  <main>
    <div class="overlay" v-show="overlay">
      <div class="modal">
        <textarea name="note" id="note" cols="30" rows="10" placeholder="Enter note..." v-model.trim="noteText"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNewNote">Add Note</button>
        <button class="close" @click="hideOverlay">Cancel</button>
      </div>
    </div>

    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showOverlay">+</button>
      </header>

      <div class="cards-container">
        <div class="card" v-for="note in noteList" :key="note.id" :style="{backgroundColor: note. backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  height: 100vh;
  width: 100vw;
  background-color: aliceblue;
  color: rgb(21, 20, 20 );
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
header button{
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20 );
  border-radius: 100%;
  color: white;
  font-size: 20px;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}
.card{
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding:  10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.date{
  font-size: 12.5px;
  font-weight: bold;
}

.cards-container{
  display: flex;
  flex-wrap: wrap;
}

.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal{
  width: 750px;
  background-color: white; 
  border-radius: 10px;
  padding: 10px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  color: white;
  border: none;
  cursor: pointer;
  margin-top: 15px;
}
.modal .close{
  background-color: red;
  margin-top: 7px;
}

.modal p {
  color: red;
}
</style>