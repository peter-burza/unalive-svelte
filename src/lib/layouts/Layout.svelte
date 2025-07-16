<script>
  import { calculateTimeLeft, getLifePercentageLived } from "../../utils";
  import Form from "../Form.svelte";
  import Portal from "../Portal.svelte";

  const { headache } = $props();

  let showModal = $state(false);
  function handleToggleModal() {
    showModal = !showModal;
  }

  let defaultName = 'Peter';
  let defaultBD = '1998-12-08';
  let defaultLE = 80;
  let birthDate = $state(defaultBD);
  let lifeExpentency = $state(defaultLE);
  let name = $state(defaultName);
  let data = $derived(calculateTimeLeft(birthDate, lifeExpentency));

  let percentage = $derived(getLifePercentageLived(birthDate, lifeExpentency));

  function handleUpdateData(n, b, e) {
    if (!n || !b || !e) return;

    // save to local storage
    localStorage.setItem("formData", JSON.stringify({ name: n, birthDate: b, lifeExpentency: e }),)

    name = n;
    birthDate = b;
    lifeExpentency = parseInt(e);
    data = calculateTimeLeft(b, parseInt(e));
    showModal = false;
  }

  function resetData() {
    name = defaultName;
    birthDate = defaultBD;
    lifeExpentency = defaultLE;
    data = calculateTimeLeft(birthDate, parseInt(lifeExpentency));
    localStorage.clear();
  }

  $effect(() => {
    const interval = setInterval(() => {
      data = calculateTimeLeft(defaultBD, parseInt(defaultLE));
    }, 1000);
    return () => clearInterval(interval)
  })

  $effect(() => {
    if (!localStorage) { return; } // Gard Close
    
    if (localStorage.getItem('formData')) {
      const {name: n, birthDate: b, lifeExpentency: e} = JSON.parse(localStorage.getItem('formData'))
    name = n;
    birthDate = b;
    lifeExpentency = parseInt(e);
    data = calculateTimeLeft(b, parseInt(e));
    }
  })

</script>

{#if showModal}
  <Portal handleCloseModal={handleToggleModal}>
    {#snippet form()}
      <Form {handleUpdateData} handleCloseModal={handleToggleModal} />
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
    resetData,
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
