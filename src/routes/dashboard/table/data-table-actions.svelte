<script lang="ts">
  import Ellipsis from "lucide-svelte/icons/ellipsis";
  import * as DropdownMenu from "$lib/components/ui/dropdown-menu";
  import { Button } from "$lib/components/ui/button";
 
  export let id: string;
</script>
 
<DropdownMenu.Root>
    <DropdownMenu.Trigger asChild let:builder>
        <Button variant="ghost" builders={[builder]} size="icon" class="relative h-8 w-8 p-0">
            <span class="sr-only">Open menu</span>
            <Ellipsis class="h-4 w-4" />
        </Button>
    </DropdownMenu.Trigger>
    <DropdownMenu.Content>
        <DropdownMenu.Group>
            <DropdownMenu.Label>Actions</DropdownMenu.Label>
                <DropdownMenu.Item on:click={() => navigator.clipboard.writeText(id)}>
                    Details
                </DropdownMenu.Item>
        </DropdownMenu.Group>
        <DropdownMenu.Separator />
        <DropdownMenu.Item>Löschen</DropdownMenu.Item>
        <DropdownMenu.Item>Bearbeiten</DropdownMenu.Item>
    </DropdownMenu.Content>
</DropdownMenu.Root>