<script setup>
import { ref } from "vue"
let id = 0;
const overlay = ref(false);
const newNote = ref("");
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

function addNote() {
  if(newNote.value === "")
  {
    alert("Notes cannot be EMPTY!!!");
    return;
  }

  notes.value.push({
    id: ++id,
    text: newNote.value,
    date: new Date(),
    color: getRandomColor()
  })
  overlay.value=false;
  newNote.value="";
}

</script>


<template>
  <main>
    <div class="overlay" v-show="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Notes</button>
        <button class="close" @click="overlay = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes {{ overlay }}</h1>
        <button @click="overlay = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note of notes" :key="note.id" class="card" :style="{backgroundColor: note.color}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">
            {{ note.date.toLocaleDateString("en-US") }}
          </p>
        </div>
      </div>
    </div>
  </main>
</template>


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
  font-size: 50px;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: black;
  border-radius: 100%;
  color: white;
  font-size: 25px;
}

.card {
  width: 225px;
  height: 225px;
  background-color: yellow;
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;

}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  justify-content: center;
  padding-top: 200px;
}

.modal {
  width: 750px;
  height: 300px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 10px;
}

.modal .close {
  background-color: red;
  margin-top: 7px;
}

.date{
  font-weight: bold;
}
</style>