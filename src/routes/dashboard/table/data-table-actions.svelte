<script lang="ts">
    import Ellipsis from "lucide-svelte/icons/ellipsis";
    import * as DropdownMenu from "$lib/components/ui/dropdown-menu";
    import * as AlertDialog from "$lib/components/ui/alert-dialog";
    import * as Dialog from "$lib/components/ui/dialog";
    import { Button } from "$lib/components/ui/button";
    import { Label } from "$lib/components/ui/label";
    import { Input } from "$lib/components/ui/input";
    import CalendarIcon from "lucide-svelte/icons/calendar";
    import {
        type DateValue,
        DateFormatter,
        getLocalTimeZone,
        CalendarDate,
    } from "@internationalized/date";
    import { cn } from "$lib/utils.js";
    import { Calendar } from "$lib/components/ui/calendar";
    import * as Popover from "$lib/components/ui/popover";

    export let id: string;
    const df = new DateFormatter("de-DE", {
        dateStyle: "short",
    });
 
    let value: DateValue | undefined = undefined
    value = new CalendarDate(2024, 4, 28)

    let deleteDialog = false;
    let detailsDialog= false;
    let editDialog = false;
</script>
 
<DropdownMenu.Root>
    <DropdownMenu.Trigger asChild let:builder>
        <Button 
            variant="ghost" 
            builders={[builder]} 
            size="icon" 
            class="relative h-8 w-8 p-0"
            >
                <Ellipsis class="h-4 w-4" />
        </Button>
    </DropdownMenu.Trigger>
    <DropdownMenu.Content>
        <DropdownMenu.Group>
            <DropdownMenu.Label>Aktionen</DropdownMenu.Label>
                <DropdownMenu.Item on:click={() => (detailsDialog= true)}>
                    Details
                </DropdownMenu.Item>
        </DropdownMenu.Group>
        <DropdownMenu.Separator />
        <DropdownMenu.Item on:click={() => (editDialog = true)}>
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

<Dialog.Root bind:open={editDialog}>
    <Dialog.Content class="sm:max-w-[425px]">
        <Dialog.Header>
          <Dialog.Title>{id}</Dialog.Title>
        </Dialog.Header>
            <div class="grid gap-4 py-6">
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="titel" class="text-right">Titel</Label>
                    <Input id="title" value="Spotify" class="col-span-3" />                
                </div>
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="value" class="text-right">Betrag</Label>
                    <Input id="value" value="17,99" class="col-span-3" />                
                </div>
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="category" class="text-right">Kategorie</Label>
                    <Input id="category" value="Freizeit" class="col-span-3" />                
                </div>
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="source" class="text-right">Quelle</Label>
                    <Input id="source" value="Paypal" class="col-span-3" />                
                </div>
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="date" class="text-right">Datum</Label>
                    <Popover.Root openFocus>
                        <Popover.Trigger asChild let:builder>
                            <Button
                                variant="outline"
                                class={cn(
                                    "w-[280px] justify-start text-left font-normal",
                                    !value && "text-muted-foreground"
                                )}
                                builders={[builder]}
                            >
                            <CalendarIcon class="mr-2 h-4 w-4" />
                            {value ? df.format(value.toDate(getLocalTimeZone())) : "Datum auswählen"}
                            </Button>
                        </Popover.Trigger>
                        <Popover.Content class="w-auto p-0">
                            <Calendar bind:value initialFocus />
                        </Popover.Content>
                    </Popover.Root>                
                </div>
            </div>
        <Dialog.Footer>
            <Button class="text-red-600" on:click={() => (editDialog = false)}>
                Abbrechen 
            </Button>
            <Button class="text-green-600" on:click={() => (editDialog = false)}>
                Bestätigen 
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
