<svelte:options tag="twopine-accordion" />

<script>
    import { slide } from "svelte/transition";
    let isOpen = false;
    const toggle = () => (isOpen = !isOpen);
    export let title;
</script>

<div>
    <button on:click={toggle} aria-expanded={isOpen}>
        {title}
        <svg
            style="tran"
            width="20"
            height="20"
            fill="none"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            viewBox="0 0 24 24"
            stroke="currentColor"><path d="M9 5l7 7-7 7" />
        </svg>
    </button>
    {#if isOpen}
        <div transition:slide={{ duration: 300 }}>
            <slot></slot>
        </div>
    {/if}
</div>

<style>
    button {
        width: 100%;
        border: none;
        background: var(--color-neutral-tint-100);
        display: block;
        color: inherit;
        cursor: pointer;
        margin: 0;
        padding-bottom: 0.5em;
        padding-top: 0.5em;
    }

    svg {
        transition: transform 0.2s ease-in;
    }

    [aria-expanded="true"] svg {
        transform: rotate(0.25turn);
    }
</style>
