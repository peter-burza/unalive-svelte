<script>
  import { calculateTimeLeft, getLifePercentageLived } from "../../utils";
  import Form from "../Form.svelte";
  import Portal from "../Portal.svelte";

  const { headache } = $props();

  let showModal = $state(false);
  function handleToggleModal() {
    showModal = !showModal;
  }
  
  let birthDate = $state("1998-12-08");
  let lifeExpentency = $state(80);
  let name = $state("peter");
  let data = $derived(calculateTimeLeft(birthDate, lifeExpentency));

  let percentage = $derived(getLifePercentageLived(birthDate, lifeExpentency));
</script>

{#if showModal}
  <Portal handleCloseModal={handleToggleModal}>
    {#snippet form()}
      <Form />
    {/snippet}
  </Portal>
{/if}

<header>
  <h1 class="text-medium text-gradient">Unalive</h1>
</header>

<main>
  {@render headache({
    data,
    birthDate,
    name,
    percentage,
    lifeExpentency,
    handleToggleModal,
  })}
</main>

<footer>
  <small>Created by</small>
  <a href="https://www.linkedin.com/in/peter-burza-695958326/" target="_blank">
    <img
      src="https://media.licdn.com/dms/image/v2/D4E03AQGBPA04VIh9FQ/profile-displayphoto-shrink_200_200/profile-displayphoto-shrink_200_200/0/1725518782193?e=1758153600&v=beta&t=YFwTNgWzp58zktNEX8n_boSdTbRalsAs3fKDO50iaHk"
      alt="pfp"
    />
    <p>@peterburza</p>
    <i class="fa-brands fa-linkedin-in"></i>
  </a>
</footer>

<style></style>
