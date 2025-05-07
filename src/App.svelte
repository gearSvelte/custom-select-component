<script lang="ts">
  import Select from './lib/Select.svelte';
  import type { TOption } from './types/option.interface';

  const options: TOption[] = [
    '',
    'red',
    { label: 'green' },
    { label: 'blue', value: 'b' },
  ];
  let selected: string | null = null;
  const handleSelect = (event: CustomEvent) => (selected = event.detail);
</script>

<main>
  <h1>Custom Select Element</h1>

  <Select {options} on:select={handleSelect} />
  {#if selected !== null}
    <div class="selected">
      You selected: <span class="selected-value">{selected}</span>
    </div>
  {/if}
</main>

<style lang="scss">
  .selected {
    margin-top: 16px;
  }
  .selected-value {
    font-weight: 700;
  }
</style>
