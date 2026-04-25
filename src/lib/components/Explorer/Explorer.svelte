<script lang="ts">
    import type { Snippet } from "svelte";
    import { createVariant } from "../../utils/builder.js";
    import { explorerConfig } from "./explorer.config.js";

    type Palette = "accent" | "tone";

    interface Props {
        palette?: Palette;
        children: Snippet;
        aria_label?: string;
    }

    let {
        palette = "tone",
        children,
        aria_label = "Explorer",
    }: Props = $props();

    const resolve = createVariant(explorerConfig);

    const root_classes = $derived(
        resolve({
            palette,
        }).trim()
    );
</script>

<nav class={root_classes} aria-label={aria_label}>
    {@render children()}
</nav>

<style>
    .explorer-component {
        display: flex;
        flex-direction: column;
        gap: 0.25rem;
        font-family: var(--font-body);
    }

    .explorer-palette-accent {
        color: var(--text-accent);
        --explorer-text: var(--text-accent);
        --explorer-muted: var(--text-accent);
        --explorer-border: var(--tone-ghost-hover);
        --explorer-hover-bg: var(--tone-ghost-hover);
        --explorer-active: var(--text-accent);
        --explorer-active-border: var(--text-accent);
    }

    .explorer-palette-tone {
        color: var(--text);
        --explorer-text: var(--text);
        --explorer-muted: var(--text-muted);
        --explorer-border: var(--tone-hover);
        --explorer-hover-bg: var(--tone-hover);
        --explorer-active: var(--accent-muted);
        --explorer-active-border: var(--accent-muted);
    }
</style>
