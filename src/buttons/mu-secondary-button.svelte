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
    background: var(--secondary-button-background, #ffffff);
    border: 1px solid var(--secondary-button-border-color, #d7dde4);
    border-radius: var(--button-border-radius, 0.45em);
    box-shadow: var(--secondary-button-box-shadow, none);
    color: var(--secondary-button-color, #1f2937);
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
    color: var(--secondary-button-color, #1f2937);
  }

  a:hover,
  button:hover:not(:disabled) {
    border-color: var(--secondary-button-hover-border-color, #6b7280);
    box-shadow: var(
      --secondary-button-hover-box-shadow,
      0 8px 18px rgba(15, 23, 42, 0.08)
    );
    transform: var(--button-hover-transform, translateY(-1px));
  }

  button:disabled {
    cursor: not-allowed;
    opacity: 0.55;
  }
</style>
