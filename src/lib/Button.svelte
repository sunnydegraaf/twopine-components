<svelte:options tag="twopine-button" />

<script>
    import { get_current_component } from "svelte/internal";
    export let type;
    export let disabled = false;

    const thisComponent = get_current_component();

    const dispatchEvent = (name, detail) => {
        thisComponent.dispatchEvent(
            new CustomEvent(name, {
                detail,
                composed: true,
            })
        );
    };

    function handleClick(event) {
        event.preventDefault();
        dispatchEvent("customClick", name);
        console.log("log");
    }
</script>

<button class={type} {disabled} on:click={handleClick}>
    <slot />
</button>

<style>
    button {
        transition: ease-in-out 0.2s all;
        box-sizing: content-box;
        padding: var(--padding);
        color: var(--color-neutral-10);
        font-size: var(--font-size);
        border-radius: var(--border-radius);
        border-width: var(--border-width);
        border-style: var(--border-style);
        border-color: var(--color-primary);
        background-color: var(--color-primary);
        cursor: pointer;
    }

    button:hover {
        transition: ease-in-out 0.2s all;
    }

    button:hover {
        background-color: var(--color-primary-hover);
    }

    button:active {
        background-color: var(--color-primary-pressed);
    }

    button:focus-visible {
        outline: var(--border-width) var(--border-style)
            var(--color-primary-focus);
    }

    button.outline:focus-visible {
        border-color: transparent;
    }

    button:disabled,
    button.secondary:disabled,
    button.outline:disabled,
    button.text:disabled,
    button[disabled] {
        border: var(--border-width) var(--border-style) var(--color-neutral-20);
        background-color: var(--color-neutral-20);
        color: var(--color-neutral-50);
        cursor: not-allowed;
    }

    button:disabled:hover,
    button.outline:disabled:hover {
        color: var(--color-neutral-50);
    }

    button.secondary:disabled:hover {
        border-color: var(--color-neutral-20);
    }

    button.secondary {
        color: var(--color-primary);
        background: var(--color-primary-bg);
        border-color: var(--color-primary-bg);
    }

    button.secondary:hover {
        transition: ease-in-out 0.2s all;
        border-color: var(--color-primary);
    }

    button.secondary:active {
        background-color: var(--color-primary-bg);
        border-color: var(--color-primary-bg);
    }

    button.outline {
        color: var(--color-primary);
        background: var(--color-primary-bg);
        border-color: var(--color-primary-border);
    }

    button.outline:hover {
        border-color: var(--color-primary-hover);
    }

    button.outline:active {
        color: var(--color-primary-pressed);
    }

    button.outline:disabled {
        border-color: var(--color-neutral-40);
    }

    button.text {
        color: var(--color-primary);
        background: transparent;
        border-color: transparent;
    }

    button.text:hover {
        border-color: var(--color-primary-hover);
    }

    button.text:active {
        color: var(--color-primary-pressed);
        border-color: transparent;
    }

    button.text:disabled {
        border-color: transparent;
        background-color: transparent;
    }
</style>
