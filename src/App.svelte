<script>
  import Calendar from "./lib/Calendar.svelte";
  import Clocks from "./lib/Clocks.svelte";
  import Hero from "./lib/Hero.svelte";
  import Layout from "./lib/layouts/Layout.svelte";
  import Summary from "./lib/Summary.svelte";
</script>

<Layout>
  {#snippet headache({ data, birthDate, name, percentage, lifeExpentency, handleToggleModal, resetData })}
    <Hero {name} {percentage} {data} {handleToggleModal} {resetData} />
    <Clocks {data} />
    <Calendar {data} {lifeExpentency} />
    <Summary {birthDate} {lifeExpentency} />
  {/snippet}
</Layout>
