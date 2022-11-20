<script>
  import { TabContent } from "sveltestrap";

  import ThemeToggle from "./lib/ThemeToggle.svelte";
  import Navbar from "./lib/Navbar.svelte";
  import Clicker from "./lib/Clicker.svelte";
  import Space from "./lib/Space.svelte";
</script>

<div style="height: 100vh;">
  <Navbar />

  <section class="py-5">
    <div class="container-fluid text-center">
      <h1 class="text-light">速度計測サイト</h1>

      <TabContent>
        <Clicker />
        <Space />
      </TabContent>
    </div>
  </section>
</div>

<ThemeToggle />
