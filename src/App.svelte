<script>
  import PovertySection from "./components/sections/poverty/poverty-section.svelte";
  import HungerSection from "./components/sections/hunger/hunger-section.svelte";
  import HealthSection from "./components/sections/health/health-section.svelte";
  import HungerPovertyTable from "./components/sections/common/charts/hunger-poverty-table.svelte";
  import Sources from "./components/sources/sources.svelte";

</script>

  <header>
    <img src="./WGS-summit-logo-transparency.png" alt="WGS Summit Logo" />
  </header>

  <h1>A Step Forward, But Still Short</h1>

  <p>
    The Sustainable Development Goals (SDGs) set by the United Nations have been
    the guiding force for global development efforts over the last decade.
    Despite the efforts of governments, organizations, and individuals around
    the world, the progress made towards achieving these goals has been uneven
    and has fallen short in many areas. This shortfall was evident even before
    the outbreak of the global pandemic, which has further exacerbated existing
    challenges and added new ones. This visual story aims to examine the
    progress made towards the SDGs and the areas where further progress is
    needed.
  </p>

  <PovertySection />

  <HungerPovertyTable />

  <HungerSection />

  <HealthSection />

  <Sources />

<style>
  @import url("https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,400;0,600;0,700&family=Hahmlet:ital,wght@0,400;0,700&family=Glass+Antiqua:ital,wght@0,400&display=swap");

  header{
    padding: 20px 20px;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
  }

  img{
    width: 200px;
  }

  h1,
  p {
    margin-left: auto;
    margin-right: auto;
    width: fit-content;
    max-width: 60ch;
  }

  p {
    color: #666;
    font-size: 20px;
    line-height: 1.4;
    letter-spacing: -0.4px;
  }
</style>
