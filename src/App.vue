<script setup>
import { ref } from 'vue';

const isVisible = ref(false);
const newNote = ref("");
const notes = ref([]);



function randomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 5000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: randomColor(),
  })
  isVisible.value = false
  newNote.value = ""
}


</script>

<template>
  <main>
    <div class="modal" v-if="isVisible">
      <div class="modal-bg" @click="isVisible = false">
      </div>
      <div class="modal-content">

        <textarea name="" id="" cols="30" rows="10" v-model="newNote"></textarea>
        <button @click="addNote()">Add notes</button>
      </div>

    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="isVisible = true">Plus</button>
      </header>
      <div class="card-wp">
        <div class="card" v-for="(note, i) in notes" :key="i">
          <p class="maintext">{{ note.text }}</p>
          <div class="date">{{ note.date }}</div>
        </div>



      </div>
    </div>


  </main>

</template>




<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

h1 {
  font-weight: bold;

}

.container {
  max-width: 80%;
  margin: 0 auto;
}

.card-wp {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
}

.card {
  flex-grow: 1;
  padding: 0.75rem;
  border-radius: 10px;
  background-color: burlywood;
  display: block;
}

.date {
  text-align: end;
  font-size: 11px;
  font-weight: bold;
}

.modal {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
  position: fixed;
  z-index: 40;
  width: 100%;
  height: 100%;
}

.modal-bg {
  bottom: 0;
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
  background-color: rgba(10, 10, 10, .86);

}

.modal-content {
  margin: 0 auto;
  max-height: calc(100vh - 40px);
  width: 640px;
  overflow: auto;
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal button {
  border: none;
  padding: 0.75rem;
  color: #000;
}
</style>