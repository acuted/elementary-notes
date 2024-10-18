<script>
  import { onMount } from 'svelte';
  import NoteList from './NoteList.svelte';
  import NoteEditor from './NoteEditor.svelte';
  import NewNoteButton from './NewNoteButton.svelte';

  let notes = [];
  let selectedNote = null;

  onMount(() => {
    const storedNotes = localStorage.getItem('notes');
    if (storedNotes) {
      notes = JSON.parse(storedNotes);
    }
  });

  function createNote(event) {
    const newNote = {
      id: Date.now(),
      title: event.detail.title,
      date: event.detail.date,
      content: ''
    };
    notes = [...notes, newNote];
    selectedNote = newNote;
    saveNotes();
  }

  function updateNote(event) {
    const updatedNote = event.detail;
    notes = notes.map(note => note.id === updatedNote.id ? updatedNote : note);
    saveNotes();
  }

  function deleteNote(event) {
    const noteId = event.detail;
    notes = notes.filter(note => note.id !== noteId);
    selectedNote = notes.length > 0 ? notes[0] : null;
    saveNotes();
  }

  function saveNotes() {
    localStorage.setItem('notes', JSON.stringify(notes));
  }
</script>

<main>
  <aside>
    <NewNoteButton on:create={createNote} />
    <NoteList {notes} bind:selectedNote on:delete={deleteNote} />
  </aside>
  <section>
    {#if selectedNote}
      <NoteEditor note={selectedNote} on:update={updateNote} on:delete={deleteNote} />
    {:else}
      <p id="not-found-note">Here it is empty ...</p>
    {/if}
  </section>
</main>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Albert+Sans:ital,wght@0,100..900;1,100..900&display=swap');
  #not-found-note {
    font-family: "Albert Sans", sans-serif;
    font-size: 48px;
    color: #cccc;
    position: absolute;
    top: 45%;
    left: 45%;
    font-weight: 400;
    text-align: center;
  }

  main {
    display: flex;
    height: 100vh;
    overflow: hidden;
  }

  aside {
    width: 300px;
    border-right: 1px solid #ccc;
  }

  section {
    flex-grow: 1;
    padding: 20px;
     overflow: hidden;
  }
</style>
