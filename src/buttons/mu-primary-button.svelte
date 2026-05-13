<script lang="ts">
  export let href: string | undefined = undefined;
  export let icon: string | undefined = undefined;
  export let name: string | undefined = undefined;
  export let type: "button" | "submit" | "reset" = "button";
  export let disabled = false;
  export let ariaLabel: string | undefined = undefined;
  export let onclick: ((event: MouseEvent) => void) | undefined = undefined;
</script>

{#if href && !disabled}
  <a {href} aria-label={ariaLabel} {onclick}>
    {#if icon}<i class={icon}></i>{/if}
    <slot
      >{#if name}{name}{/if}</slot
    >
  </a>
{:else}
  <button {type} {disabled} aria-label={ariaLabel} {onclick}>
    {#if icon}<i class={icon}></i>{/if}
    <slot
      >{#if name}{name}{/if}</slot
    >
  </button>
{/if}

<style>
  a,
  button {
    align-items: center;
    background: var(
      --button-background,
      linear-gradient(135deg, rgba(23, 105, 244, 0.95), rgba(25, 199, 213, 0.9))
    );
    border: 1px solid var(--button-border-color, rgba(232, 251, 255, 0.18));
    border-radius: var(--button-border-radius, 0.45em);
    box-shadow: var(--button-box-shadow, 0 8px 20px rgba(22, 153, 242, 0.18));
    color: var(--color-primary-contract, #e8fbff);
    display: inline-flex;
    gap: 0.35em;
    margin: 0;
    padding: var(--button-padding, 0.55em 0.75em);
    text-decoration: none;
    transition: var(
      --button-transition,
      border-color 120ms ease,
      box-shadow 120ms ease,
      transform 120ms ease
    );
  }

  a:visited {
    color: var(--color-primary-contract, #e8fbff);
  }

  a:hover,
  button:hover:not(:disabled) {
    border-color: var(--button-hover-border-color, rgba(232, 251, 255, 0.5));
    box-shadow: var(
      --button-hover-box-shadow,
      0 10px 28px rgba(25, 199, 213, 0.28)
    );
    transform: var(--button-hover-transform, translateY(-1px));
  }

  button:disabled {
    cursor: not-allowed;
    opacity: 0.55;
  }
</style>
