<script lang="ts">
  interface Props {
    items?: string[];
    inputId?: string;
  }

  let { items = $bindable([]), inputId = "tagsInput" }: Props = $props();
  let value = $state("");

  const onKeydown = (e: KeyboardEvent) => {
    if (e.code == "Enter" && value != "" && e.isComposing == false) {
      if (!items.includes(value)) {
        var i = items;
        i.push(value);
        items = i;
        value = "";
      }
    }
  };
  const onBlur = () => {
    if (value == "" || items.includes(value)) {
      return;
    }
    var i = items;
    i.push(value);
    items = i;
    value = "";
  };
  const deleteClick = (e: MouseEvent) => {
    const t = e.target as HTMLButtonElement;
    items = items.filter((value) => value != t.dataset.value);
  };
</script>

<section>
  <div>
    {#each items as i}
      <span>
        {i}
        <button
          aria-label={`delete tag ${i}`}
          data-value={i}
          onclick={deleteClick}
        ></button>
      </span>
    {/each}
  </div>
  <input
    id={inputId}
    type="text"
    placeholder="タグ（複数指定可）"
    bind:value
    onkeydown={onKeydown}
    onblur={onBlur}
  />
</section>

<style>
  section {
    align-items: center;
    display: flex;
    gap: 0.5rem;
    width: 100%;
  }

  div {
    display: flex;
    flex-wrap: wrap;
    gap: 0.35rem;
  }

  span {
    align-items: center;
    background: #1b2030;
    border: 1px solid #394152;
    border-radius: 999px;
    color: #eef2ff;
    display: inline-flex;
    font-size: 1rem;
    gap: 0.35rem;
    line-height: 1;
    min-height: 2rem;
    padding: 0 0.35rem 0 0.75rem;
  }

  button {
    align-items: center;
    background: #5e6a7d;
    border: 0;
    border-radius: 999px;
    color: #ffffff;
    cursor: pointer;
    display: inline-flex;
    height: 1.25rem;
    justify-content: center;
    padding: 0;
    width: 1.25rem;
  }

  button::before {
    content: "x";
    font-size: 0.8rem;
    line-height: 1;
  }

  button:hover {
    background: #7a8798;
  }

  input {
    border: 1px solid #394152;
    border-radius: 0.35rem;
    background-color: #161b28;
    background-image: linear-gradient(180deg, #1b2030, #161b28);
    color: #eef2ff;
    caret-color: #8ec5ff;
    flex: 1 1 12rem;
    min-height: 2.35rem;
    min-width: 8rem;
    padding: 0 0.65rem;
  }

  input:focus {
    border-color: #5ea7f0;
    box-shadow: 0 0 0 0.15rem rgba(94, 167, 240, 0.28);
    outline: none;
  }

  input::placeholder {
    color: rgba(238, 242, 255, 0.52);
  }
</style>
