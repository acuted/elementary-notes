<script>
  import { createEventDispatcher } from 'svelte';

  export let notes = [];
  export let selectedNote = null;

  const dispatch = createEventDispatcher();

  function selectNote(note) {
    selectedNote = note;
  }

  function deleteNote(noteId) {
    dispatch('delete', noteId);
  }
</script>

<div class="note-list">
  {#each notes as note (note.id)}
    <div
      class="note-item"
      class:selected={selectedNote && selectedNote.id === note.id}
      on:click={() => selectNote(note)}
    >
    <div id="note-details">
      <span class="note-title">{note.title}</span>
      <span class="note-date">{note.date}</span>
    </div>
      <button class="delete-btn" on:click|stopPropagation={() => deleteNote(note.id)}>🗑️</button>
    </div>
  {/each}
</div>

<style>
  
  @import url('https://fonts.googleapis.com/css2?family=Albert+Sans:ital,wght@0,100..900;1,100..900&display=swap');
  
  .note-list {
    font-family: 'Albert Sans', sans-serif;
    height: calc(100% - 50px);
    overflow-y: auto;
  }
  
  #note-details {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .note-item {
    padding: 10px;
    border-bottom: 1px solid #eee;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .note-item.selected {
    background-color: #f0f0f0;
  }

  .note-title {
    font-size: 14px;
    font-weight: bold;
  }

  .note-date {
    font-size: 0.8em;
    color: #888;
  }

  .delete-btn {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 1.2em;
  }
</style>
