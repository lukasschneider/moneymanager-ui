<script lang="ts">
    import {
            DashboardMainNav,
            UserNav,
        } from "./index.js";
    import * as Card from "$lib/components/ui/card/index.js";
    import * as Tabs from "$lib/components/ui/tabs/index.js";
    import HandCoins from "lucide-svelte/icons/hand-coins";
    import Plus from "lucide-svelte/icons/plus";
    import LandMark from "lucide-svelte/icons/landmark";
    import TrendingDown from "lucide-svelte/icons/trending-down";
    import TrendingUp from "lucide-svelte/icons/trending-up";
    import Overview from "./overview.svelte";
    import RecentTransactions from "./recent-transactions.svelte";
    import DataTable from "./table/data-table.svelte";
    import * as Dialog from "$lib/components/ui/dialog";
    import { Button } from "$lib/components/ui/button";
    import { Label } from "$lib/components/ui/label";
    import { Input } from "$lib/components/ui/input";
    import CalendarIcon from "lucide-svelte/icons/calendar";
    import {
        type DateValue,
        DateFormatter,
        getLocalTimeZone,
    } from "@internationalized/date";
    import { cn } from "$lib/utils.js";
    import { Calendar } from "$lib/components/ui/calendar";
    import * as Popover from "$lib/components/ui/popover";

    const df = new DateFormatter("de-DE", {
        dateStyle: "short",
    });
 
    let value: DateValue | undefined = undefined

    let newEntryDalog = false;

    export let incomesData = [
        {
            id: "1",
            title: "Gehalt",
            source: "Arbeitgeber",
            category: "Gehalt",
            date: "28.04.2024",
            value: 3000,
        },
        {
            id: "2",
            title: "Zinsen",
            category: "Bankdepot",
            source: "Bank",
            date: "28.04.2024",
            value: 200,
        },
    ];

    export let expenseData = [
        {
            id: "25",
            title: "Spotify",
            source: "Paypal",
            category: "Abonnements",
            date: "28.04.2024",
            value: 17.99,
        },
        {
            id: "13",
            title: "Amazon Prime",
            category: "Abonnements",
            source: "Bank",
            date: "28.04.2024",
            value: 8.99,
        },
        {
            id: "20",
            title: "Discord Nitro",
            category: "Abonnements",
            source: "Paypal",
            date: "28.04.2024",
            value: 2.99,
        },
        {
            id: "19",
            title: "Disney Plus",
            category: "Abonnements",
            source: "Paypal",
            date: "28.04.2024",
            value: 8.99,
        },
    ];
</script>

<div class="hidden flex-col sm:flex lg:flex md:flex">
	<div class="border-b">
		<div class="flex h-16 items-center px-4">
			<DashboardMainNav currentSite='dashboard' />
			<div class="ml-auto flex items-center space-x-4">
				<UserNav />
			</div>
		</div>
	</div>
    <div class="flex-1 sm:flex-1 md:flex-1 lg:flex-1 space-y-4 p-8 pt-6">
		<div class="flex items-center justify-between space-y-2">
			<h2 class="text-3xl font-bold tracking-tight">Dashboard</h2>
			<div class="flex items-center space-x-2">
				<Button size="sm" on:click={() => (newEntryDalog = true)}>
                    <Plus class="h-4 w-4" />
                    Neuer Eintrag
				</Button>
			</div>
		</div>
		<Tabs.Root value="overview" class="space-y-4">
			<Tabs.List>
				<Tabs.Trigger value="overview">Übersicht</Tabs.Trigger>
				<Tabs.Trigger value="incomes" >Einnahmen</Tabs.Trigger>
				<Tabs.Trigger value="expense" >Ausgaben</Tabs.Trigger>
			</Tabs.List>
            <Tabs.Content value="incomes">
                <DataTable bind:data={incomesData}/>
            </Tabs.Content>
            <Tabs.Content value="expense">
                <DataTable bind:data={expenseData}/>
            </Tabs.Content>
			<Tabs.Content value="overview" class="space-y-4">
				<div class="grid gap-4 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-4">
					<Card.Root>
						<Card.Header
							class="flex flex-row items-center justify-between space-y-0 pb-2"
						>
							<Card.Title class="text-sm font-medium">Kontostand</Card.Title>
							<LandMark class="h-5 w-5 text-muted-foreground" />
						</Card.Header>
						<Card.Content>
							<div class="text-2xl font-bold">+3.500,20 €</div>
							<p class="text-xs text-muted-foreground">+50.1% von letztem Monat</p>
						</Card.Content>
					</Card.Root>
					<Card.Root>
						<Card.Header
							class="flex flex-row items-center justify-between space-y-0 pb-2"
						>
							<Card.Title class="text-sm font-medium">Ausgaben</Card.Title>
							<TrendingDown class="h-4 w-4 text-muted-foreground" />
						</Card.Header>
						<Card.Content>
							<div class="text-2xl font-bold">-400 €</div>
							<p class="text-xs text-muted-foreground">-10% im Vergleich zu letztem Monat</p>
						</Card.Content>
					</Card.Root>
					<Card.Root>
						<Card.Header
							class="flex flex-row items-center justify-between space-y-0 pb-2"
						>
							<Card.Title class="text-sm font-medium">Einnahmen</Card.Title>
							<TrendingUp class="h-4 w-4 text-muted-foreground" />
						</Card.Header>
						<Card.Content>
							<div class="text-2xl font-bold">+1500 €</div>
							<p class="text-xs text-muted-foreground">0% im Vergleich zum letztem Monat</p>
						</Card.Content>
					</Card.Root>
					<Card.Root>
						<Card.Header
							class="flex flex-row items-center justify-between space-y-0 pb-2"
						>
							<Card.Title class="text-sm font-medium">Geld pro Monat nach Fixkosten</Card.Title>
							<HandCoins class="h-4 w-4 text-muted-foreground" />
						</Card.Header>
						<Card.Content>
							<div class="text-2xl font-bold">978 €</div>
							<p class="text-xs text-muted-foreground">-50€ weniger als im Letzten Monat</p>
						</Card.Content>
					</Card.Root>
				</div>
				<div class="grid gap-4 sm:grid-cols-2 md:grid-cols-2 lg:grid-cols-7">
					<Card.Root class="col-span-4">
						<Card.Header>
							<Card.Title>Ausgaben</Card.Title>
							<Card.Description>Ausgaben in diesem Jahr</Card.Description>
						</Card.Header>
						<Card.Content>
                            <Overview />
						</Card.Content>
					</Card.Root>
					<Card.Root class="col-span-3">
						<Card.Header>
							<Card.Title>Buchungen</Card.Title>
							<Card.Description>Es gibt 250 Buchungen diesen Monat</Card.Description>
						</Card.Header>
						<Card.Content>
                            <RecentTransactions />
						</Card.Content>
					</Card.Root>
				</div>
			</Tabs.Content>
		</Tabs.Root>
	</div>
</div>

<Dialog.Root bind:open={newEntryDalog}>
    <Dialog.Content class="sm:max-w-[425px]">
        <Dialog.Header>
          <Dialog.Title>Neuer Eintrag</Dialog.Title>
        </Dialog.Header>
            <div class="grid gap-4 py-6">
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="titel" class="text-right">Titel</Label>
                    <Input id="title" placeholder="Titel" class="col-span-3" />                
                </div>
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="value" class="text-right">Betrag</Label>
                    <Input id="value" placeholder="Betrag" class="col-span-3" />                
                </div>
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="category" class="text-right">Kategorie</Label>
                    <Input id="category" placeholder="Kategorie" class="col-span-3" />                
                </div>
                <div class="grid grid-cols-4 items-center gap-4">
                    <Label for="source" class="text-right">Quelle</Label>
                    <Input id="source" placeholder="Quelle" class="col-span-3" />                
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
            <Button class="text-red-600" on:click={() => (newEntryDalog = false)}>
                Abbrechen 
            </Button>
            <Button class="text-green-600" on:click={() => (newEntryDalog = false)}>
                Bestätigen 
            </Button>
        </Dialog.Footer>
    </Dialog.Content>
</Dialog.Root>
