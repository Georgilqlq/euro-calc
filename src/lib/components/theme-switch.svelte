<script lang="ts">
	import { onMount } from 'svelte';

    const Themes = {
	LIGHT: 'light',
	DARK: 'dark'};

    type themeType = typeof Themes[keyof typeof Themes];
    const storageItem: string = 'theme';
	let theme: themeType = Themes.LIGHT;

    function changeTheme(value: themeType) {
        if(!document.startViewTransition) {
            applyNewTheme(value);
            return;
        }

        document.startViewTransition(() => {
            applyNewTheme(value);
        })
    }

	function applyNewTheme(value: themeType) {
		document.documentElement.setAttribute('data-bs-theme', value);
		localStorage.setItem(storageItem, value);
		theme = value;
	}

	function toggleTheme() {
        switch(theme){
            case Themes.DARK:
                changeTheme(Themes.LIGHT);
                break;
            case Themes.LIGHT:
                changeTheme(Themes.DARK);
                break;
        }
	}

	onMount(() => {
		const savedTheme = localStorage.getItem(storageItem) as themeType | null;

		if (savedTheme) {
			applyNewTheme(savedTheme);
		} else {
			const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
			applyNewTheme(prefersDark ? Themes.DARK : Themes.LIGHT);
		}
	});
</script>

<button class="btn btn-outline-secondary d-flex align-items-center gap-2" on:click={toggleTheme}>
	{#if theme === Themes.DARK}
		<span class="d-none d-sm-inline">☾</span>
	{:else}
		<span class="d-none d-sm-inline">☼</span>
	{/if}
</button>