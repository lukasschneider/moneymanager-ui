<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import { Label } from "$lib/components/ui/label/index.js";
    import { Input } from "$lib/components/ui/input/index.js";
</script>
<div class="flex min-h-full flex-col justify-center px-7 py-12 lg:px-8">
  <div class="sm:mx-auto sm:w-full sm:max-w-sm">
    <h2 class="mt-10 text-center text-2xl font-bold leading-9">Anmelden</h2>
  </div>
  <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
    <form class="space-y-6" action="?/login" method="POST">
      <div>
        <Label for="email-2">Email</Label>
        <div class="mt-2">
            <Input type="email" id="email-2" name="email" placeholder="Email" />
            <p class="text-sm text-muted-foreground">Enter your email address.</p>
        </div>
      </div>
      <div>
        <div class="flex items-center justify-between">
        <Label for="password-2">Email</Label>
        </div>
        <div class="mt-2">
            <Input type="password" name="password" id="password-2" placeholder="Passwort" />
            <p class="text-sm text-muted-foreground">Bitte gib dein Passwort ein</p>
        </div>
      </div>
      <div>
          <Button class="w-full" href="/dashboard">Anmelden</Button>
      </div>
    </form>
  </div>
</div>
