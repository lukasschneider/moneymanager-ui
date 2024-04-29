<script lang="ts">
    import Ellipsis from "lucide-svelte/icons/ellipsis";
    import * as DropdownMenu from "$lib/components/ui/dropdown-menu";
    import * as AlertDialog from "$lib/components/ui/alert-dialog";
    import * as Dialog from "$lib/components/ui/dialog";
    import { Button } from "$lib/components/ui/button";

    export let id: string;
    let deleteDialog = false;
    let detailsDialog= false;



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
                <DropdownMenu.Item on:click={() => (detailsDialog= true)}>
                    Details
                </DropdownMenu.Item>
        </DropdownMenu.Group>
        <DropdownMenu.Separator />
        <DropdownMenu.Item>
            Bearbeiten 
        </DropdownMenu.Item>
        <DropdownMenu.Item class="text-red-700" on:click={() => (deleteDialog = true)}>
            Löschen 
        </DropdownMenu.Item>
    </DropdownMenu.Content>
</DropdownMenu.Root>
 
<Dialog.Root bind:open={detailsDialog}>
    <Dialog.Content class="sm:max-w-[425px]">
        <Dialog.Header>
          <Dialog.Title>{id}</Dialog.Title>
        </Dialog.Header>
            <div class="grid gap-4 py-6">
                <div class="grid grid-cols-2 items-center gap-4">
                    <div class="font-bold">Titel</div>
                    <div>Spotify</div>
                </div>
                <div class="grid grid-cols-2 items-center gap-4">
                    <div class="font-bold">Betrag</div>
                    <div>17.99</div>
                </div>
                <div class="grid grid-cols-2 items-center gap-4">
                    <div class="font-bold">Kategorie</div>
                    <div>Freizeit</div>
                </div>
                <div class="grid grid-cols-2 items-center gap-4">
                    <div class="font-bold">Quelle</div>
                    <div>Paypal</div>
                </div>
                <div class="grid grid-cols-2 items-center gap-4">
                    <div class="font-bold">Datum</div>
                    <div>28.04.2024</div>
                </div>
            </div>
        <Dialog.Footer>
            <Button on:click={() => (detailsDialog= false)}>
                Fertig
            </Button>
        </Dialog.Footer>
    </Dialog.Content>
</Dialog.Root>

<AlertDialog.Root bind:open={deleteDialog}>
    <AlertDialog.Content>
        <AlertDialog.Header>
            <AlertDialog.Title>Sind sie sicher?</AlertDialog.Title>
            <AlertDialog.Description>
                Diese Aktion kann nicht rückgängig gemacht werden!
            </AlertDialog.Description>
        </AlertDialog.Header>
            <AlertDialog.Footer>
                <AlertDialog.Cancel>Abbrechen</AlertDialog.Cancel>
                <AlertDialog.Action class="text-red-700">Bestätigen</AlertDialog.Action>
            </AlertDialog.Footer>
    </AlertDialog.Content>
</AlertDialog.Root>



