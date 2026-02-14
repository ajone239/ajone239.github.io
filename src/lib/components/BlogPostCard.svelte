<script lang="ts">
    const { entry, hover = true } = $props();

    const { path, meta } = entry;
    const title = meta.title ? meta.title : path;
</script>

<div class="container">
    <div class={['card', { hover }]}>
        {#if meta.date}
            <p class="date">
                Published: {meta.date}
            </p>
        {/if}

        <h2>
            <a href={path}>
                {title}
                <span></span>
            </a>
        </h2>

        {#if meta.excerpt}
            <p>
                <b><em>TL;DR:</em></b>
                {meta.excerpt}
            </p>
        {/if}
    </div>
</div>

<style lang="scss">
    .container {
        border-bottom: 2px solid var(--main-border-color);
        position: relative;
        .card {
            margin: 1px;
            padding: 5px;
            border-radius: 8px;

            &.hover:hover {
                background: var(--hover-bg-color);
            }
        }
        .date {
            opacity: 0.5;
        }

        a {
            color: inherit;
        }

        span {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;

            z-index: 1;
        }
    }
</style>
