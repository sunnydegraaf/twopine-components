<svelte:options tag="twopine-card" />

<script>

</script>

<div class="card">
    <slot name="badge" class="badge"/>
    <div class="image-container">
        <slot name="image" class="image"/>
    </div>
    <div class="info">
        <slot name="title"/>
        <slot name="button"/>
    </div>
</div>

<style>
    .card {
        background-color: var(--color-secundary);
        position: relative;
        border-radius: var(--border-radius);
        box-shadow: var(--box-shadow);
    }

    .card .image::slotted(img) {
        width: 100%;
        padding: 15% 20%;
        transition: 0.2s;
        transform: scale(1);
    }

    .card .image::slotted(img:hover) {
        transform: scale(1.05);
    }

    .badge {
        position: absolute;
        top: 5%;
        left: -10px;
    }

    .info {
        width: 100%;
        position: absolute;
        bottom: 5%;
        left: -10px;
    }

    .badge::slotted(twopine-badge) {
        position: absolute;
        top: 5%;
        left: -10px;
    }
</style>
