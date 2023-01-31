<script setup>
import { defineComponent, ref } from "vue"
import overlayModule from "./overlayModule.vue"

let id = 0;
const overlay = ref(false);
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const  addNote =(e,val) => {
  
  console.log(e,val);
  if(val === "")
  {
    alert("Notes cannot be EMPTY!!!");
    return;
  }

  notes.value.push({
    id: ++id,
    text: val,
    date: new Date(),
    color: getRandomColor()
  })
  overlay.value=false;
}


</script>


<template>
  <main>
    <overlayModule :overlay="overlay" @close-modal="overlay=false" @send-text="addNote"/>
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