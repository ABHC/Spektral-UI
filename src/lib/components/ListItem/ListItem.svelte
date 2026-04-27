<script lang="ts">
    import type { Snippet } from 'svelte';
    import { createVariant } from "../../utils/builder.js";
    import { listItemConfig } from './listItem.config.js';

    type Size = "sm" | "md" | "lg";
    type Palette = "tone" | "accent" | "ghost" | "neutral" | "error" | "warning" | "success" | "info";
    type Elevation = "none" | "subtle" | "hard";

    interface Props {
        label: string;
        size?: Size;
        palette?: Palette;
        elevation?: Elevation;
        rounded?: boolean;
        active?: boolean;
        leading?: Snippet;
        trailing?: Snippet;
        children?: Snippet;
        onclick?: () => void;
    }

    let {
        label,
        size = "md",
        palette = "tone",
        elevation = "none",
        rounded = false,
        active = false,
        leading,
        trailing,
        children,
        onclick,
    }: Props = $props();

    const resolve = createVariant(listItemConfig);
    const wrapper_classes = $derived(
        resolve({
            size,
            palette,
            elevation,
            rounded: rounded ? true : undefined,
            active: active ? true : undefined,
        }).trim()
    );
</script>

{#snippet content()}
    {#if leading}
        <div class="leading">
            {@render leading()}
        </div>
    {/if}

    <div class="supporting-text">
        <div class="main-supporting">
            {label}
        </div>
        {#if children}
            <div class="extra-supporting">
                {@render children()}
            </div>
        {/if}
    </div>

    {#if trailing}
        <div class="trailing">
            {@render trailing()}
        </div>
    {/if}
{/snippet}

{#if onclick}
    <button class="{wrapper_classes}" {onclick}>
        {@render content()}
    </button>
{:else}
    <div class="{wrapper_classes}">
        {@render content()}
    </div>
{/if}

<style>
    /* Reset button styles */
    button.list-item {
        font: inherit;
        text-align: inherit;
        width: 100%;
        cursor: pointer;
    }

    button.list-item:focus { outline: none; }
    button.list-item:focus-visible {
        outline: var(--spk-focus-ring-width) solid var(--spk-focus-ring);
        outline-offset: var(--spk-focus-ring-offset);
    }

    /* Base */
    .list-item {
        display: flex;
        align-items: center;
        gap: 0.75rem;
        border: var(--spk-border) solid transparent;
        transition: background var(--spk-duration-base) ease, border-color var(--spk-duration-base) ease, box-shadow var(--spk-duration-base) ease;
    }

    /* Palette - tone ---------------------------------------------------- */

    .list-item-tone {
        background: var(--spk-tone);
        color: var(--spk-text);
    }

    button.list-item-tone:hover {
        background: var(--spk-tone-hover);
    }

    button.list-item-tone.list-item-active {
        border-color: var(--spk-accent);
    }

    /* Palette - accent -------------------------------------------------- */

    .list-item-accent {
        background: var(--spk-accent);
        color: var(--spk-text-accent);
    }

    button.list-item-accent:hover {
        background: var(--spk-accent-hover);
    }

    button.list-item-accent.list-item-active {
        border-color: var(--spk-accent-muted);
    }

    /* Palette - ghost (adapts to context via currentColor) -------------- */

    .list-item-ghost {
        background: color-mix(in srgb, currentColor 8%, transparent);
        color: inherit;
    }

    button.list-item-ghost:hover {
        background: color-mix(in srgb, currentColor 15%, transparent);
    }

    button.list-item-ghost.list-item-active {
        border-color: color-mix(in srgb, currentColor 30%, transparent);
    }

    /* Palette - error --------------------------------------------------- */

    .list-item-error {
        background: var(--spk-error);
        color: var(--spk-text-error);
    }

    button.list-item-error:hover {
        background: var(--spk-error-hover);
    }

    button.list-item-error.list-item-active {
        border-color: var(--spk-error-muted);
    }

    /* Palette - warning ------------------------------------------------- */

    .list-item-warning {
        background: var(--spk-warning);
        color: var(--spk-text-warning);
    }

    button.list-item-warning:hover {
        background: var(--spk-warning-hover);
    }

    button.list-item-warning.list-item-active {
        border-color: var(--spk-warning-muted);
    }

    /* Palette - success ------------------------------------------------- */

    .list-item-success {
        background: var(--spk-success);
        color: var(--spk-text-success);
    }

    button.list-item-success:hover {
        background: var(--spk-success-hover);
    }

    button.list-item-success.list-item-active {
        border-color: var(--spk-success-muted);
    }

    /* Palette - info ---------------------------------------------------- */

    .list-item-info {
        background: var(--spk-info);
        color: var(--spk-text-info);
    }

    button.list-item-info:hover {
        background: var(--spk-info-hover);
    }

    button.list-item-info.list-item-active {
        border-color: var(--spk-info-muted);
    }

    /* Palette - neutral ------------------------------------------------- */

    .list-item-neutral {
        background: var(--spk-neutral);
        color: var(--spk-text-neutral);
    }

    button.list-item-neutral:hover {
        background: var(--spk-neutral-hover);
    }

    button.list-item-neutral.list-item-active {
        border-color: var(--spk-neutral-muted);
    }

    /* Elevation --------------------------------------------------------- */

    .list-item-elevation-subtle {
        box-shadow: var(--spk-elevation-subtle) var(--spk-shadow-subtle);
    }

    .list-item-elevation-hard {
        box-shadow: var(--spk-elevation-hard) var(--spk-shadow-hard);
    }

    /* Rounded ----------------------------------------------------------- */

    .list-item-rounded {
        border-radius: var(--spk-radius-soft);
    }

    /* Inner elements ---------------------------------------------------- */

    .leading {
        display: flex;
        align-items: center;
        flex-shrink: 0;
    }

    .trailing {
        display: flex;
        align-items: center;
        flex-shrink: 0;
        margin-left: auto;
    }

    .supporting-text {
        flex: 1;
        min-width: 0;
    }

    .main-supporting {
        font-weight: 600;
        line-height: 1.2;
    }

    .extra-supporting {
        font-size: 0.8em;
        opacity: var(--spk-opacity-muted);
        margin-top: 0.1rem;
        white-space: pre-line;
    }

    /* Sizes ------------------------------------------------------------- */

    /* small */
    .list-item-sm {
        padding: 0.35rem 0.6rem;
    }

    .list-item-sm .main-supporting {
        font-weight: 500;
        font-size: 0.8rem;
    }

    .list-item-sm .extra-supporting {
        font-size: 0.7rem;
    }

    /* medium */
    .list-item-md {
        padding: 0.6rem 0.9rem;
    }

    .list-item-md .main-supporting {
        font-weight: 600;
    }

    .list-item-md .extra-supporting {
        font-size: 0.8em;
    }

    /* large */
    .list-item-lg {
        padding: 0.9rem 1.25rem;
        font-size: 1.05rem;
    }

    .list-item-lg .main-supporting {
        font-weight: 700;
        font-size: 1.1rem;
    }

    .list-item-lg .extra-supporting {
        font-size: 0.9em;
    }
</style>
