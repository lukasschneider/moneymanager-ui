<script lang="ts">
    import * as Avatar from "$lib/components/ui/avatar/index.js";
    const data = [
        {
            type: "expense",
            date: "27.04.2024",
            value: "80,00",
            name: "Konzert"
        },
        {
            type: "income",
            date: "27.04.2024",
            value: "2500,00",
            name: "Gehalt"
        },
        {
            type: "expense",
            date: "27.04.2024",
            value: "80,00",
            name: "Konzert"
        },
        {
            type: "expense",
            date: "27.04.2024",
            value: "80,00",
            name: "Konzert"
        },
        {
            type: "expense",
            date: "27.04.2024",
            value: "80,00",
            name: "Konzert"
        },
    ];
</script>

<div class="space-y-8">
    {#each data as d}
    <div class="flex items-center">
        <Avatar.Root class="h-9 w-9">
        {#if d.type == "income"}
            <Avatar.Fallback>E</Avatar.Fallback>
        {:else if d.type == "expense"}
            <Avatar.Fallback>A</Avatar.Fallback>
        {:else}
            <Avatar.Fallback></Avatar.Fallback>
        {/if}
		</Avatar.Root>
        <div class="ml-4 space-y-1">
            <p class="text-sm font-medium leading-none">{ d.name }</p>
            <p class="text-sm text-muted-foreground">{ d.date}</p>
        </div>
        {#if d.type == "income"}
            <div class="ml-auto text-green-600 font-medium">+{d.value} €</div>
        {:else if d.type == "expense"}
            <div class="ml-auto text-red-600 font-medium">-{d.value} €</div>
        {:else}
            <div class="ml-auto font-medium">{d.value} €</div>
        {/if}
    </div>
    {/each}
</div>
