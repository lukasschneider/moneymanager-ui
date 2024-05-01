<script lang="ts">
    import Package2 from "lucide-svelte/icons/package-2";
	let site: string | undefined | null = undefined;
	export { site as currentSite};
</script>

<nav class="flex items-center space-x-4 sm:space-x-4 md:space-x-4 lg:space-x-6">
    <a href="##" class="flex items-center gap-2 text-lg font-semibold md:text-base">
        <Package2 class="h-6 w-6" />
        <span class="sr-only">Acme Inc</span>
      </a>
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
