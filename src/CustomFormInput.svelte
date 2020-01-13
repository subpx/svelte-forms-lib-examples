<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  const options = ['Male', 'Female'];
  let selected;

  $: {
    dispatch('change', selected);
  }

  function select(value) {
    selected = value;
  }
</script>

<style>
  .customInput {
    display: flex;
  }

  .customInput > div {
    border: 1px solid black;
    cursor: pointer;
    padding: 5px;
    margin: 0 2px;
  }

  .selected {
    background: black;
    color: white;
  }
</style>

<div class="customInput">
{ #each options as option }
  <div class:selected="{ selected === option }" on:click="{ () => select(option) }">{ option }</div>
{ /each }
</div>
