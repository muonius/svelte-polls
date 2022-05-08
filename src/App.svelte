<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import Tabs from "./shared/Tabs.svelte";
  //tabs
  let items = ["Current Polls", "Add New Poll"];
  let activeItem = "Current Polls";
  const tabChange = (e) => {
    activeItem = e.detail;
  };
</script>

<Header />
<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange} />
  {#if activeItem === "Current Polls"}
    <p>poll list goes here</p>
  {:else if activeItem === "Add New Poll"}
    <CreatePollForm />
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 940px;
    margin: 40px auto;
  }
</style>
