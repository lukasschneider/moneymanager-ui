<script lang="ts">
    import { Button } from "$lib/components/ui/button/index.js";
    import * as Card from "$lib/components/ui/card/index.js";
    import { Input } from "$lib/components/ui/input/index.js";
    import { Label } from "$lib/components/ui/label/index.js";
    import { DashboardMainNav } from "../dashboard";
    import { UserNav } from "../dashboard";
</script>

<div class="flex min-h-screen w-full flex-col">
	<div class="border-b">
		<div class="flex h-16 items-center px-4">
			<DashboardMainNav />
			<div class="ml-auto flex items-center space-x-4">
				<UserNav />
			</div>
		</div>
	</div>
    <main class="flex min-h-[calc(100vh_-_theme(spacing.16))] flex-1 flex-col gap-4 bg-muted/40 p-4 md:gap-8 md:p-10">
        <div class="mx-auto grid w-full max-w-6xl gap-2">
            <h1 class="text-3xl font-semibold">Einstellungen</h1>
        </div>
        <div class="mx-auto grid w-full max-w-6xl items-start gap-6 md:grid-cols-[180px_1fr] lg:grid-cols-[250px_1fr]">
            <nav class="grid gap-4 text-sm text-muted-foreground" data-x-chunk-container="chunk-container after:right-0">
                <p class="font-semibold text-primary">Persönliche Einstellungen</p>
            </nav>
            <div class="grid gap-6">
                <Card.Root>
                    <Card.Header>
                        <Card.Title>Namen ändern</Card.Title>
                    </Card.Header>
                    <Card.Content>
                        <form>
                            <Label>Vorname</Label>
                            <div class="mt-2 mb-2">
                                <Input placeholder="Vorname" />
                            </div>
                            <Label>Nachname</Label>
                            <div class="mt-2 mb-2">
                                <Input placeholder="Nachname" />
                            </div>
                        </form>
                    </Card.Content>
                    <Card.Footer class="border-t px-6 py-4">
                        <Button>Speichern</Button>
                    </Card.Footer>
                </Card.Root>
                <Card.Root>
                    <Card.Header>
                        <Card.Title>Email-Adresse ändern</Card.Title>
                    </Card.Header>
                    <Card.Content>
                        <form>
                            <Label>Email-Adresse</Label>
                            <div class="mt-2 mb-2">
                                <Input placeholder="Email-Adresse" />
                            </div>
                            <Label>Email-Adresse wiederholen</Label>
                            <div class="mt-2 mb-2">
                                <Input placeholder="Email-Adresse wiederholen" />
                            </div>
                        </form>
                    </Card.Content>
                    <Card.Footer class="border-t px-6 py-4">
                        <Button>Speichern</Button>
                    </Card.Footer>
                </Card.Root>
                <Card.Root>
                    <Card.Header>
                        <Card.Title>Passwort ändern</Card.Title>
                    </Card.Header>
                    <Card.Content>
                        <form>
                            <Label>Altes Passwort</Label>
                            <div class="mt-2 mb-2">
                                <Input placeholder="Altes Passwort" />
                            </div>
                            <Label>Neues Passwort</Label>
                            <div class="mt-2 mb-2">
                                <Input placeholder="Neues Passwort" />
                            </div>
                            <Label>Neues Passwort wiederholen</Label>
                            <div class="mt-2 mb-2">
                                <Input placeholder="Neues Passwort wiederholen" />
                            </div>
                        </form>
                    </Card.Content>
                    <Card.Footer class="border-t px-6 py-4">
                        <Button>Speichern</Button>
                    </Card.Footer>
                </Card.Root>
            </div>
        </div>
  </main>
</div>
