<script>
import Navbar from '$lib/Navbar.svelte';
</script>

<img src="banner.png" alt="banner" />
<Navbar />

<main>
    <slot />
</main>

  <style>

img {
  width: 100%;
  height: auto;
  margin: 0;
  padding: 0;
  display: block;
}
main {
    margin: 0 auto;
    max-width: 960px;
    padding: 16px;
}
</style>
