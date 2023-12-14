<script setup>
import { ref } from "vue";
const noteTitle = ref("");
const noteBody = ref("");
const resetNote = () => {
  noteTitle.value = "";
  noteBody.value = "";
};

const createNote = () => {
  const newNote = { title: noteTitle.value, body: noteBody.value, updatedAt: new Date() };
  fetch("http://localhost:3000/notes/", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(newNote),
  })
    .then((res) => res.json())
    .then((data) => console.log());
  resetNote();
};
function refresh() {
  location.reload();
}
</script>

<template>
  <div>
    <h1>Vue Notes</h1>
    <form @submit.prevent="createNote">
      <div class="newTitle">
        <label name="title">Title</label>
        <input v-model="noteTitle" id="title" name="title" />
      </div>
      <br />
      <div>
        <label name="body">Body</label>
        <textarea v-model="noteBody" id="body" name="body"> </textarea>
      </div>
      <button for="btn" action="submit" @click="refresh()">New Note</button>
    </form>
  </div>
</template>
