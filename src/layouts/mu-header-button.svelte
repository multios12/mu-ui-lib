<script context="module" lang="ts">
  export type HeaderButtonConfig = {
    name?: string;
    href: string;
    icon?: string;
    position?: HeaderButtonPosition;
  };

  export type HeaderButtonPosition =
    | "before-title"
    | "after-sub-title"
    | "before-logout"
    | "after-logout";
</script>

<script lang="ts">
  import PrimaryButton from "../buttons/mu-primary-button.svelte";

  export let button: HeaderButtonConfig | undefined = undefined;
  export let position: HeaderButtonPosition;
</script>

{#if button && (button.position ?? "before-title") === position}
  <PrimaryButton href={button.href} icon={button.icon} name={button.name} />
{/if}
