<script lang="ts">
	import { cn } from "$lib/utils.js";

	let className: string | undefined | null = undefined;
	export { className as class };
</script>

<nav class={cn("flex items-center space-x-4 lg:space-x-6", className)}>
	<a href="/dashboard" class="text-sm font-medium transition-colors hover:text-primary">
        Dashboard
	</a>

	<a
		href="/incomes"
		class="text-sm font-medium text-muted-foreground transition-colors hover:text-primary"
	>
		Einnahmen
	</a>
	<a
		href="/expense"
		class="text-sm font-medium text-muted-foreground transition-colors hover:text-primary"
	>
		Ausgaben
	</a>
	<a
		href="/settings"
		class="text-sm font-medium text-muted-foreground transition-colors hover:text-primary"
	>
        Einstellungen
	</a>
</nav>
