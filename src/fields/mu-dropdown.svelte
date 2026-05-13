<script lang="ts">
  interface Props {
    /** 選択アイテムのリスト */
    items: { key: string; value: string }[];
    /** 表示値のキー */
    key?: string;
    tabindex: number | null | undefined;
    onchange?: (value: string) => void;
  }

  let { items, key = $bindable(""), tabindex, onchange }: Props = $props();
  $effect(() => {
    if (items.length > 0 && !items.some((item) => item.key === key)) {
      key = items[0].key;
    }
  });

  const onChange = (event: Event) => {
    const nextKey = (event.currentTarget as HTMLSelectElement).value;
    key = nextKey;
    onchange?.(nextKey);
  };
</script>

<div>
  <select bind:value={key} {tabindex} onchange={onChange}>
    {#each items as item}
      <option value={item.key}>{item.value}</option>
    {/each}
  </select>
</div>

<style>
  div {
    display: flex;
    align-items: center;
  }

  select {
    border: 1px solid #d7dde4;
    border-radius: 0.35rem;
    min-height: 2.35rem;
    line-height: 1.2;
    padding: 0 2rem 0 0.65rem;
  }
</style>
