<script lang="ts">
  interface Props {
    hasUnsavedChanges?: boolean;
    statusLabel?: string;
  }

  let { hasUnsavedChanges = false, statusLabel = "未保存の変更あり" }: Props =
    $props();
</script>

<footer>
  <div>
    <div data-visible={hasUnsavedChanges}>
      {#if hasUnsavedChanges}
        <span>{statusLabel}</span>
      {/if}
    </div>
    <div>
      <slot />
    </div>
  </div>
</footer>

<style>
  footer {
    background-color: #353a36;
    bottom: 0;
    left: 0;
    margin: 0;
    position: fixed;
    width: 100%;
  }

  footer > div {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0.35rem;
    padding: 0.45rem 0.7rem;
  }

  footer > div > div {
    display: flex;
    align-items: center;
  }

  [data-visible="true"] {
    min-height: 2rem;
  }

  footer > div > div:last-child {
    gap: 0.35rem;
    margin-left: auto;
  }

  span {
    color: #b15b12;
    user-select: none;
  }

  @media screen and (max-width: 768px) {
    footer > div {
      flex-wrap: wrap;
      gap: 0.4rem;
      padding: 0.45rem 0.75rem 0.6rem;
    }

    footer > div > div {
      width: 100%;
    }

    footer > div > div:first-child {
      min-height: 0;
    }

    footer > div > div:last-child {
      justify-content: space-between;
      gap: 0.5rem;
    }

    [data-visible="true"] {
      min-height: 1.2rem;
    }

    span {
      font-size: 0.8rem;
      line-height: 1.1;
    }
  }
</style>
