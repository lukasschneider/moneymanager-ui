<script lang="ts">
import {
		DashboardMainNav,
		UserNav,

	} from "./index.js";
import * as Card from "$lib/components/ui/card/index.js";
import * as Tabs from "$lib/components/ui/tabs/index.js";
import Activity from "lucide-svelte/icons/activity";
import CreditCard from "lucide-svelte/icons/credit-card";
import DollarSign from "lucide-svelte/icons/dollar-sign";
import Users from "lucide-svelte/icons/users";
    import Overview from "./overview.svelte";
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
			</div>
		</div>
		<Tabs.Root value="overview" class="space-y-4">
			<Tabs.List>
				<Tabs.Trigger value="overview">Übersicht</Tabs.Trigger>
				<Tabs.Trigger value="incomes" >Einnahmen</Tabs.Trigger>
				<Tabs.Trigger value="expense" >Ausgaben</Tabs.Trigger>
			</Tabs.List>
			<Tabs.Content value="overview" class="space-y-4">
				<div class="grid gap-4 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-4">
					<Card.Root>
						<Card.Header
							class="flex flex-row items-center justify-between space-y-0 pb-2"
						>
							<Card.Title class="text-sm font-medium">Kontostand</Card.Title>
							<DollarSign class="h-4 w-4 text-muted-foreground" />
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
							<Users class="h-4 w-4 text-muted-foreground" />
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
							<CreditCard class="h-4 w-4 text-muted-foreground" />
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
							<Activity class="h-4 w-4 text-muted-foreground" />
						</Card.Header>
						<Card.Content>
							<div class="text-2xl font-bold">978 €</div>
							<p class="text-xs text-muted-foreground">-50€ weniger als im Letzten Monat</p>
						</Card.Content>
					</Card.Root>
				</div>
				<div class="grid gap-4 md:grid-cols-2 lg:grid-cols-7">
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
							<Card.Title>Recent Sales</Card.Title>
							<Card.Description>You made 265 sales this month.</Card.Description>
						</Card.Header>
						<Card.Content>
						</Card.Content>
					</Card.Root>
				</div>
			</Tabs.Content>
		</Tabs.Root>
	</div>
</div>
