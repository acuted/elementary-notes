<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let isExpanded = false;
  let title = '';
  let date = new Date().toISOString().split('T')[0];

  function toggleExpand() {
    isExpanded = !isExpanded;
  }

  function createNote() {
    if (title && date) {
      dispatch('create', { title, date });
      title = '';
      date = new Date().toISOString().split('T')[0];
      isExpanded = false;
    }
  }
</script>

<div class="new-note-button" class:expanded={isExpanded}>
  {#if !isExpanded}
    <button on:click={toggleExpand}>New Notes</button>
  {:else}
    <input bind:value={title} placeholder="Enter a title and for the modify " />
    <input type="date" bind:value={date} />
    <button on:click={createNote}>Create</button>
  {/if}
</div>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Albert+Sans:ital,wght@0,100..900;1,100..900&display=swap');

  .new-note-button {
    margin-top: 6px;
    padding: 10px;
    transition: height 0.3s ease-in-out;
  }

  .new-note-button.expanded {
    height: 155px;
    z-index: 999;
    position: absolute;
    /*background-color: #383333;*/
    background-color: #f0f1f2;
    border-radius: 5px;
    width: 270px;
    
  }

  input, button {
    outline: none;
    cursor: pointer;
    color: #161616;
    font-family: 'Albert Sans', sans-serif;
    display: block;
    width: 100%;
    font-weight: 600;
    padding: 10px;
    border-radius: 5px;
    margin-bottom: 10px;
    /*background-color: #383333;*/
    /*box-shadow: rgba(50, 50, 93, 0.25) 0px 30px 60px -12px inset, rgba(0, 0, 0, 0.3) 0px 18px 36px -18px inset;*/
  }
</style>
