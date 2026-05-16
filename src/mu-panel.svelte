<script lang="ts">
  import MuPrimaryButton from "./buttons/mu-primary-button.svelte";

  export let title: string;
  export let sites: Array<{ name: string; href: string; icon?: string }> = [];
</script>

<section>
  <h2>{title}</h2>
  <div>
    {#each sites as site}
      <MuPrimaryButton href={site.href} icon={site.icon} name={site.name} />
    {/each}
    <br />
    <br />
  </div>
</section>

<style>
  section {
    background-color: var(--panel-bg-color, #081425);
    border-color: var(--panel-border-color, #174782);
    border-radius: var(--panel-border-radius, 0.5em);
    border-style: solid;
    border-width: var(--panel-border-width, 1px);
    box-shadow: var(--panel-box-shadow, 0 18px 45px rgba(0, 0, 0, 0.36));
    margin: var(--panel-margin, 2em);
  }

  h2 {
    color: var(--color-primary, #19c7d5);
    font-size: 1rem;
    font-weight: 600;
    margin: 0.25em;
  }

  div {
    display: flex;
    flex-wrap: wrap;
    gap: var(--panel-content-gap, 0.75em);
    margin: 1em;
  }
</style>
