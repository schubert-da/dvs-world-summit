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
  The <strong>Sustainable Development Goals</strong> (SDGs) set by the United Nations
  have been the guiding force for global development efforts over the last decade.
  While initial progress was made in the early years, progress started to plateau
  in many critical areas, leaving nations grappling with the sobering reality of
  falling behind in their efforts to achieve these targets.
</p>

<p>
  This shortfall was evident even before the outbreak of the <strong>global pandemic</strong>, 
  which has further exacerbated existing challenges and added new ones. This
  visual story aims to examine the progress made towards few key SDGs and how global progress 
  evolved over time.
</p>

<PovertySection />

<HungerSection />

<HungerPovertyTable />

<HealthSection />

<Sources />

<style>
  @import url("https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,400;0,600;0,700&family=Hahmlet:ital,wght@0,400;0,700&family=Glass+Antiqua:ital,wght@0,400&display=swap");

  header {
    padding: 20px 20px;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
  }

  img {
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
