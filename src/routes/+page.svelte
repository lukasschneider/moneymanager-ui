<script lang="ts">
    import { goto } from "$app/navigation";
    import { onMount } from "svelte";
    let user = { isLoggedIn : true }
    if (user.isLoggedIn) {
        onMount(() => {
            goto('/dashboard')
        });
    } else {
        onMount(() => {
            goto('/login')
        });
    }

</script>
