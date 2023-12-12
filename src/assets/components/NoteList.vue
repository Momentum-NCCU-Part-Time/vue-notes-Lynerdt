<script setup>
import { ref } from "vue";
const notes = ref([]);
const apiURL = "http://localhost:3000/notes/";

const deleteNote = (id) => {
  return fetch(`${apiURL}/${id}`, {
    method: "DELETE",
  }).then((response) => response.json());
};

const removeNote = (noteId) => {
  deleteNote(noteId).then(removeDeletedNote(noteId));
};
const removeDeletedNote = (noteId) => {
  notes.value = notes.value.filter((note) => note.id !== noteId);
};

fetch("http://localhost:3000/notes/", {
  method: "GET",
  headers: { "Content-Type": "application/json" },
})
  .then((res) => res.json())
  .then((data) => (notes.value = data));
</script>
<template>
  <NewNote />
  <div class="allNotes">
    <div class="notecards" v-for="note in notes" :key="note.id">
      <h1 class="notestitle">{{ note.title }}</h1>

      <h2 class="notesbody">{{ note.body }}</h2>
      <button type="submit" id="editbutton">EDIT</button>
      <button @click.prevent="removeNote(note.id)">DELETE</button>
    </div>
  </div>
</template>
