<svelte:options tag="twopine-modal" />

<script>
    import { fade } from "svelte/transition";
    export let id = "";
    export let show = false;
    function close(e) {
        dispatchCloseEvent.call(this, e);
        show = false;
    }
    function dispatchCloseEvent(e) {
        const event = new CustomEvent("close", {
            detail: `modal-element was closed.`,
            bubbles: true,
            cancelable: true,
            composed: true, // makes the event jump shadow DOM boundary
        });

        this.dispatchEvent(event);
    }
    let closePath = `M28.228,23.986L47.092,5.122c1.172-1.171,1.172-3.071,0-4.242c-1.172-1.172-3.07-1.172-4.242,0L23.986,19.744L5.121,0.88
        c-1.172-1.172-3.07-1.172-4.242,0c-1.172,1.171-1.172,3.071,0,4.242l18.865,18.864L0.879,42.85c-1.172,1.171-1.172,3.071,0,4.242
        C1.465,47.677,2.233,47.97,3,47.97s1.535-0.293,2.121-0.879l18.865-18.864L42.85,47.091c0.586,0.586,1.354,0.879,2.121,0.879
        s1.535-0.293,2.121-0.879c1.172-1.171,1.172-3.071,0-4.242L28.228,23.986z`;
</script>

{#if show}
    <div
        transition:fade={{ duration: 200 }}
        class="modal"
        id="modal"
    >
        <div class="modal-guts">
            <slot />
        </div>

        <span class="close-button" on:click={close} role="button">
            <slot name="close">
                <svg
                    height="12px"
                    width="12px"
                    viewBox="0 0 47.971 47.971"
                    style="enable-background:new 0 0 47.971 47.971;"
                >
                    <g>
                        <path d={closePath} />
                    </g>
                </svg>
            </slot>
        </span>
    </div>

    <div class="modal-overlay" id="modal-overlay" on:click={close} />
{/if}

<style>
    .modal {
        width: var(--size-x-large);
        height: var(--size-large);
        display: flex;
        max-width: 100%;
        max-height: 100%;
        position: fixed;
        z-index: 100;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        background: var(--color-neutral-10);
        box-shadow: 0 0 60px 10px rgba(0, 0, 0, 0.1);
    }

    .modal.error {
        
    }

    .modal-overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 50;
        background: rgba(64, 63, 63, 0.6);
    }
    .modal-guts {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        overflow: auto;
        padding: var(--padding-medium);
    }
    .modal .close-button {
        position: absolute;
        z-index: 1;
        top: 15px;
        right: 15px;
        cursor: pointer;
    }
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }
</style>
