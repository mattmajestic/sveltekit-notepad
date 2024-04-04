<script>
  import { onMount } from 'svelte';
  import Button from '@smui/button';

  let noteText = '';
  let notes = [];
  let inputElement;

  function addNote() {
    if (noteText.trim()) {
      notes.push(noteText);
      noteText = '';
    }
  }

  function handleKeydown(event) {
    if (event.key === 'Enter') {
      event.preventDefault();
      addNote();
    }
  }

  onMount(() => {
    inputElement.focus();
  });
</script>

<svelte:head>
  <title>Notepad</title>
  <meta name="description" content="Smart notepad application" />
</svelte:head>

<div class="text-column">
  <h1>Smart Notepad</h1>

  <div class="input-area">
    <input
      type="text"
      bind:value={noteText}
      on:keydown={handleKeydown}
      placeholder="Type your note here..."
      bind:this={inputElement}
    />
    <Button on:click={addNote}>Enter</Button>
  </div>

  {#if notes.length > 0}
    <div class="latest-note">
      <h2>Latest Note</h2>
      <p>{notes[notes.length - 1]}</p>
    </div>
  {/if}

  <div class="notes-display">
    <h2>All Notes</h2>
    {#each notes as note, i (i)}
      <div class="note" key={i}>
        <p>{note}</p>
      </div>
    {/each}
  </div>
</div>

<style>
  .input-area {
    display: flex;
    align-items: center;
    margin-top: 1rem;
  }

  .latest-note {
    margin-top: 1rem;
  }

  .notes-display {
    margin-top: 2rem;
  }

  .note {
    margin-bottom: 0.5rem;
    background-color: var(--mdc-theme-surface, #f0f0f0);
    padding: 10px;
    border-radius: 4px;
  }

  .text-column {
    max-width: 800px;
    margin: auto;
  }

  input[type="text"] {
    flex-grow: 1;
    margin-right: 8px;
  }
</style>
