<script lang="ts">
    import { SiteTitle } from "$lib/info";
    import type { MenuLink } from "$lib/types/MenuLink";
    import { slide } from "svelte/transition";

    let { menuLinks }: { menuLinks: MenuLink[] } = $props();

    let open = $state(false);

    let buttonText = $derived(open ? "close" : "open");
</script>

<div class="header-container">
    <div class="header-content">
        <h3>
            <a href="/">{SiteTitle}</a>
        </h3>

        <button onclick={() => (open = !open)}>
            {buttonText}
        </button>
    </div>

    <!-- TODO: is this good for accessibility? -->
    {#if open}
        <div class="menu" transition:slide>
            <aside>
                <nav>
                    <ul>
                        {#each menuLinks as menuLink (menuLink.title)}
                            <li>
                                <a
                                    class="nav-links"
                                    href={menuLink.url}
                                    onclick={() => (open = false)}
                                >
                                    {menuLink.title}
                                </a>
                            </li>
                        {:else}
                            <li>
                                <p>There's no links :(</p>
                            </li>
                        {/each}
                    </ul>
                </nav>
            </aside>
        </div>
    {/if}
</div>

<style lang="scss">
    .header-container {
        flex-direction: column;
        flex: 1;
        align-items: center;
        border-bottom: 2px solid lightgrey;
    }
    .header-content {
        padding: 0.5rem;
        display: flex;
        flex: 1;
        align-items: center;
        justify-content: space-between;
    }
    h3 {
        margin: 10px;
    }
    a {
        color: inherit;
        &.nav-links {
            &::before {
                content: "[  ";
            }
            &::after {
                content: "  ]";
            }
            text-decoration: underline;
            font-weight: bold;
        }
    }
    aside {
        border-top: dashed lightgrey 2px;
        padding: 5px;
        display: flex;
        justify-content: center;
    }
    ul {
        list-style: none;
        display: contents;
        border: solid red 1px;
    }
    li {
        margin-bottom: 10px;
        text-align: center;
    }
</style>
