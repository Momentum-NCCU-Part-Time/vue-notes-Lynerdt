<script setup>
import { ref } from "vue";
const noteTitle = ref("");
const noteBody = ref("");

fetch("http://localhost:3000/notes/", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ title, body, updatedAt: new Date() }),
})
  .then((res) => res.json())
  .then((data) => console.log(data));
</script>

<template>
  <form id="writeNotes">
    <h2>Saved Notes</h2>

    <label name="title" id="title">Title of Notes</label>
    <input :value="text" @input="(event) => (text = event.target.value)" />

    <label name="body" id="body">Body of Notes</label>
    <textarea v-model="text" />

    <button for="btn" action="submit">Post Your Thoughts</button>
  </form>
</template>
