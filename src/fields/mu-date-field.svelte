<script lang="ts">
  interface Props {
    editable?: boolean;
    inputId?: string;
    value: string;
  }

  let {
    editable = false,
    inputId = "dateInput",
    value = $bindable(""),
  }: Props = $props();
</script>

{#if editable}
  <input id={inputId} type="date" bind:value={value} />
{:else}
  <time datetime={value}>{value}</time>
{/if}

<style>
  input,
  time {
    width: 100%;
    min-width: 9.5rem;
    min-height: 2.2rem;
  }

  input {
    border: 1px solid #d7dde4;
    border-radius: 0.35rem;
    height: 2.2rem;
    padding: 0 0.6rem;
  }

  time {
    display: inline-flex;
    align-items: center;
    color: #1f2937;
    font-variant-numeric: tabular-nums;
    font-size: 1.2rem;
    font-weight: 700;
    letter-spacing: 0.02em;
    line-height: 1;
  }
</style>
