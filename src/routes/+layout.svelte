<script>
import Navbar from '$lib/Navbar.svelte';
</script>

<Navbar />

<main>
    <slot />
</main>

  <style>
main {
    margin: 0 auto;
    max-width: 960px;
    padding: 16px;
}
</style>
