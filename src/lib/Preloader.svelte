<svelte:options tag="twopine-preloader" />

<script>
    // Component props
    let loading
    
    // preload animation
    let setLoading = () => {
        setTimeout(() => {
            loading = "loading"
        }, 100);
    }
</script>

<div on:load={setLoading()} class="{loading} preloader product-teaser">
    <div class="preloader-background" />
    <div class="preloader-msg">
        <span class="preloader-logo">
            <slot/>
        </span>
    </div>
</div>

<style>
    .preloader {
        position: fixed;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        z-index: 1000;
        transition: opacity 1s cubic-bezier(0.2, 0.6, 0.35, 1) 2.4s,
            visibility 1s cubic-bezier(0.2, 0.6, 0.35, 1) 2.4s,
            transform 1s cubic-bezier(0.5, 0.05, 0.7, 0.2) 1.8s;
        opacity: 1;
        visibility: visible;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
    }

    .preloader-background {
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        background-color: var(--color-primary);
        transform-origin: center top;
        transition: transform 0.8s cubic-bezier(0.77, 0, 0.175, 1) 2s;
    }

    .preloader-msg {
        text-align: center;
        transition: transform 0.6s cubic-bezier(0.5, 0.05, 0.7, 0.2) 2s,
            opacity 0.4s cubic-bezier(0.2, 0.6, 0.35, 1) 2.2s;
        width: 100%;
        position: relative;
    }

    .preloader-msg span {
        color: #fff;
        position: relative;
        width: 100%;
        max-width: 160px;
        display: flex;
        margin-left: auto;
        margin-right: auto;
    }

    .preloader-msg slot {
        width: 100%;
        fill: #fff;
    }

    .preloader-msg::after {
        content: "";
        position: absolute;
        top: -1px;
        left: 0;
        bottom: -1px;
        right: 0;
        background-color: var(--color-primary);
        opacity: 1;
        transform-origin: right;
        transition: transform 1.2s cubic-bezier(0.5, 0.05, 0.7, 0.2);
    }

    .loading.preloader {
        opacity: 0;
        visibility: hidden;
        transform: translateY(-100%);
    }

    .loading.preloader-background {
        transform: scaleY(0.0001);
        transition-delay: 2.2s;
    }

    .loading.preloader-msg {
        opacity: 0;
        transform: translateY(-60px);
    }

    .loading .preloader-msg::after {
        transform: scaleX(0);
    }
</style>
