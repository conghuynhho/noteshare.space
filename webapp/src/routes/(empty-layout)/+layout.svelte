<script lang="ts">
    import { browser } from '$app/environment';
    import '../../app.css';

    let dark: boolean;
    let darkTheme = 'dark';

    $: getTheme();

    $: {
        if (browser) {
            window.localStorage.setItem('isDarkMode', String(dark));
        }
    }

    async function getTheme() {
        if (browser) {
            const savedMode = window.localStorage.getItem('isDarkMode');
            dark = savedMode ? savedMode === 'true' : false;
            window.localStorage.setItem('isDarkMode', String(dark));
        }
    }
</script>

<svelte:head>
    <title>{import.meta.env.VITE_BRANDING} — Securely share your Obsidian notes with one click.</title
    >
    <meta
            name="title"
            content="Noteshare.space — Securely share your Obsidian notes with one click."
    />
    <meta
            name="description"
            content="Securely share your Obsidian notes with one click. Zero configuration. End-to-end encrypted. No account needed. Completely open source! Download the QuickShare extension in the Obsidian community plugin marketplace."
    />

    <!-- Open Graph / Facebook -->
    <meta property="og:type" content="website" />
    <meta property="og:url" content="https://noteshare.space/" />
    <meta
            property="og:title"
            content="Noteshare.space — Securely share your Obsidian notes with one click."
    />
    <meta
            property="og:description"
            content="Securely share your Obsidian notes with one click. Zero configuration. End-to-end encrypted. No account needed. Completely open source! Download the QuickShare extension in the Obsidian community plugin marketplace."
    />
    <meta property="og:image" content="https://noteshare.space/meta.png" />

    <!-- Twitter -->
    <meta property="twitter:card" content="summary_large_image" />
    <meta property="twitter:url" content="https://noteshare.space/" />
    <meta
            property="twitter:title"
            content="Noteshare.space — Securely share your Obsidian notes with one click."
    />
    <meta
            property="twitter:description"
            content="Securely share your Obsidian notes with one click. Zero configuration. End-to-end encrypted. No account needed. Completely open source! Download the QuickShare extension in the Obsidian community plugin marketplace."
    />
    <meta property="twitter:image" content="https://noteshare.space/meta.png" />
</svelte:head>

<div class=" h-full {dark !== undefined ? '' : 'hidden'} {dark ? darkTheme : ''}">
    <div class="bg-white dark:bg-background-dark min-h-full transition-colors">

        <div class="container">
            <slot />
        </div>
    </div>
</div>
