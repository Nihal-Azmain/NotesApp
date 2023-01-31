<script setup>
    import { ref } from "vue";
    const prop = defineProps(['overlay']);
    const emit = defineEmits(['closeModal','sendText']);
    const newNote =ref("");
    const onNoteClick=(e)=>{
      emit("sendText",e,newNote.value);
      newNote.value="";
    }
    const onCloseClick=(e)=>{
      emit("closeModal");
      newNote.value="";
    }
</script>



<template>
    <div class="overlay" v-show="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="onNoteClick">Add Notes</button>
        <button class="close" @click="onCloseClick">Close</button>
      </div>
    </div>
</template>




<style scoped>
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

</style>