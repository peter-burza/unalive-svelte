<script>
  let { lifeExpentency, birthDate } = $props();
  const finalYear = $derived(parseInt(birthDate.split("-")[0]) + lifeExpentency);
</script>

<section id="summary">
    <div>
        <p class="text-gradinet">
            <i class="fa-solid fa-heart-crack"></i>
            You'll probably die in the year <strong>{finalYear}</strong> at the age of <strong>{lifeExpentency}</strong>
        </p>
    </div>
    <h4>Yesterday is histopy, tomorrow is a mystery, and today is a gift. That's why they call it the present.</h4>
    <h4>Master Oogway</h4>
</section>
