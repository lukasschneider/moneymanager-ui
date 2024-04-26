<script lang="ts">
	import { cn } from "$lib/utils.js";

	let site: string | undefined | null = undefined;
	export { site as currentSite};
</script>

<nav class="flex items-center space-x-4 sm:space-x-4 md:space-x-4 lg:space-x-6">
    {#if site == 'dashboard'}
	<a  
        href="/dashboard" 
        class="text-sm font-medium transition-colors hover:text-primary"
    > 
        Dashboard
	</a>
    {:else}
	<a
		href="/dashboard"
		class="text-sm font-medium text-muted-foreground transition-colors hover:text-primary"
	>
	    Dashboard	
	</a>
    {/if}

    {#if site == 'incomes'}
	<a  
        href="/incomes" 
        class="text-sm font-medium transition-colors hover:text-primary"
    > 
        Einnahmen 
	</a>
    {:else}
	<a
		href="/incomes"
		class="text-sm font-medium text-muted-foreground transition-colors hover:text-primary"
	>
	    Einnahmen 
	</a>
    {/if}
    {#if site == 'expense'}
	<a  
        href="/expense"
        class="text-sm font-medium transition-colors hover:text-primary"
    > 
        Ausgaben
	</a>
    {:else}
	<a
		href="/expense"
		class="text-sm font-medium text-muted-foreground transition-colors hover:text-primary"
	>
	    Ausgaben 
	</a>
    {/if}
</nav>
