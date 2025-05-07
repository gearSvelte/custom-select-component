<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import type { TOption } from '../types/option.interface';
  const dispatch = createEventDispatcher();
  export let options;

  const getLabel = (option: TOption) =>
    typeof option === 'object' ? option.label : option;

  const getValue = (option: TOption) =>
    typeof option === 'object' ? option.value || option.label : option;
</script>

<select
  on:change={(event) =>
    dispatch('select', (event.target as HTMLSelectElement).value)}
>
  {#each options as option}
    <option value={getValue(option)}>{getLabel(option)}</option>
  {/each}
</select>

<style lang="scss"></style>
