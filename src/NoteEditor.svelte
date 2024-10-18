<script>
  import { createEventDispatcher } from 'svelte';

  export let note;

  const dispatch = createEventDispatcher();

  $: if (note) {
    dispatch('update', note);
  }

  function deleteNote() {
    dispatch('delete', note.id);
  }
</script>

<div class="note-editor">
  <input
    bind:value={note.title}
    placeholder="Title"
    class="note-title"
  />
<span style="height: 2px; background-color: #cccc;"></span>
  <textarea
    bind:value={note.content}
    placeholder="Write your note here... to change the title just click on it and write again."
    class="note-content"
  ></textarea>
  <div style="display: flex; align-items: center; justify-content: space-between;">
    <button class="delete-btn" on:click={deleteNote}>Delete Note</button>
    <span>You are using the Elementary Notes in the version 1.0.0</span>
  </div>
</div>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Albert+Sans:ital,wght@0,100..900;1,100..900&display=swap');
  .note-editor {
    display: flex;
    flex-direction: column;
    height: 100%;
    overflow: hidden;
  }

  .note-title {
    font-size: 1.2em;
    margin-bottom: 10px;
    padding: 5px;
    border: none;
    font-weight: bold;
    outline: none;
  }

  .note-content {
    flex-grow: 1;
    padding: 10px;
    font-size: 1em;
    resize: none;
    border: none;
    font-family: "Albert Sans", sans-serif;
    outline: none;
  }
  
  .note-content a {
    color: #00008B;
    text-decoration: underline;
  }

  .delete-btn {
    box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
    align-self: flex-start;
    margin-top: 10px;
    padding: 10px;
    background-color: #ff4444;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    transition: background ease-in-out .3s;
  }
  
  .delete-btn:hover {
    transition: background ease-in-out .3s;
    background-color: #992f2f;
  }
</style>
