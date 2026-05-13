<script context="module" lang="ts">
  export type HeaderTab = {
    id?: string;
    label: string;
    href?: string;
    active?: boolean;
    disabled?: boolean;
  };
</script>

<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import HeaderButton from "./mu-header-button.svelte";
  import type { HeaderButtonConfig } from "./mu-header-button.svelte";

  export let title: string;
  export let subTitle: string;
  export let headerButton: HeaderButtonConfig | undefined = undefined;
  export let logoutHref = "auth/api/logout";
  export let tabs: HeaderTab[] = [];
  export let activeTab: string | undefined = undefined;

  const dispatch = createEventDispatcher<{ tabselect: HeaderTab }>();

  function isActive(tab: HeaderTab) {
    return tab.active || (!!activeTab && (tab.id ?? tab.label) === activeTab);
  }

  function selectTab(tab: HeaderTab) {
    if (!tab.disabled) {
      dispatch("tabselect", tab);
    }
  }
</script>

<header>
  <div>
    <span>
      <HeaderButton button={headerButton} position="before-title" />{title}
    </span>
    <span>{subTitle}</span>
    {#if tabs.length > 0}
      <nav aria-label="Header tabs">
        {#each tabs as tab}
          {#if tab.href && !tab.disabled}
            <a
              href={tab.href}
              role="tab"
              aria-selected={isActive(tab)}
              onclick={() => selectTab(tab)}
            >
              {tab.label}
            </a>
          {:else}
            <button
              type="button"
              role="tab"
              aria-selected={isActive(tab)}
              disabled={tab.disabled}
              onclick={() => selectTab(tab)}
            >
              {tab.label}
            </button>
          {/if}
        {/each}
      </nav>
    {/if}
    <HeaderButton button={headerButton} position="after-sub-title" />
    <HeaderButton button={headerButton} position="before-logout" />
    <a href={logoutHref} aria-label="Logout"
      ><span class="material-icons">logout</span></a
    >
    <HeaderButton button={headerButton} position="after-logout" />
  </div>
</header>

<style>
  header {
    background: var(--header-background);
    border-bottom: 1px solid var(--header-border-color);
    box-shadow: var(--header-box-shadow);
    color: var(--color-primary-contract);
    margin-bottom: var(--header-margin-bottom);
    padding: var(--header-padding);
  }

  header > div {
    align-items: center;
    display: flex;
    gap: 0.7em;
  }

  header > div > span:first-child {
    color: var(--color-primary-contract);
    font-family: "Anton", sans-serif;
    font-weight: 700;
    font-size: 1.5em;
  }

  header > div > span:nth-child(2) {
    color: var(--header-sub-title-color);
  }

  a[aria-label="Logout"] {
    color: var(--header-link-color);
    margin: 0.25em 0.25em 0.25em auto;
    padding: 0;
    text-align: right;
  }

  a[aria-label="Logout"]:visited {
    color: var(--color-primary-contract);
  }

  nav {
    align-items: center;
    display: flex;
    flex-wrap: wrap;
    gap: var(--header-tab-gap, 1em);
    margin-left: var(--header-tab-margin-left, 0.5em);
  }

  [role="tab"] {
    background: transparent;
    border: 0;
    border-bottom: 2px solid transparent;
    color: var(--header-sub-title-color);
    cursor: pointer;
    font: inherit;
    line-height: 1.4;
    padding: var(--header-tab-padding, 0.15em 0 0.25em);
    text-decoration: none;
  }

  a[role="tab"]:visited {
    color: var(--header-sub-title-color);
  }

  [role="tab"]:hover {
    color: var(--color-primary-contract);
  }

  [role="tab"][aria-selected="true"] {
    border-bottom-color: var(
      --header-tab-active-border-color,
      var(--color-primary)
    );
    color: var(--color-primary-contract);
  }

  button[role="tab"]:disabled {
    cursor: not-allowed;
    opacity: 0.45;
  }
</style>
