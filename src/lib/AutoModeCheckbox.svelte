<script lang="ts">
  import Checkbox from '@smui/checkbox';
  import FormField from '@smui/form-field';
  import Tooltip, { Wrapper } from '@smui/tooltip';
  import { onMount } from 'svelte';
  let autoMode = false;

  onMount(() => {
    chrome?.storage?.sync?.get(['autoMode', 'mode'], (result) => {
      autoMode = result.autoMode == null ? false : result.autoMode;
    });
  });

  const checkboxUpdate = () => {
    autoMode = !autoMode;
    chrome?.storage?.sync?.set({ autoMode });
  };
</script>

<FormField>
  <Wrapper>
    <FormField>
      <Checkbox on:click={checkboxUpdate} bind:checked={autoMode} touch />
      <span slot="label" tabindex="0">Auto Mode</span>
    </FormField>
    <Tooltip unbounded>Attempt to Trigger Automatically</Tooltip>
  </Wrapper>
</FormField>
