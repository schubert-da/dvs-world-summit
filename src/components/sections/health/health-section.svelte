<script>
    import DiseaseBarCharts from "./charts/disease-bar-charts.svelte";
    import LifeExpectancyMaps from "./charts/life-expectancy-maps.svelte";
    import HealthTable from "../common/charts/health-table.svelte";
    import Scrolly from "../common/utils/scrolly.svelte";

    let currentStep;
</script>

<div class="section poverty-section">
    <Scrolly bind:value={currentStep}>
        <div class="step" class:active={currentStep >= 0}>
            <h1>Health and Well-being</h1>

            <p>
                Major progress has been made in improving the health of millions
                of people, increasing life expectancy, reducing maternal and
                child mortality and fighting against leading communicable
                diseases.
            </p>

            <p>
                However, progress has stalled or is not happening fast enough
                with regard to addressing major diseases, such as malaria and
                tuberculosis, while at least half the global population does not
                have access to essential health services and many of those who
                do suffer undue financial hardship, potentially pushing them
                into extreme poverty.
            </p>
        </div>

        <div class="step" class:active={currentStep >= 1}>
            <DiseaseBarCharts />
        </div>

        <div class="step" class:active={currentStep >= 2}>
            <p>
                Life expectancy is the most commonly used measure used to
                describe a population's health. Historical data shows that
                global life expectancy has increased drastically over the last
                couple of centuries, with substantial long-run improvements in
                all countries around the world.
            </p>
        </div>

        <div class="step" class:active={currentStep >=2}>
            <LifeExpectancyMaps />
        </div>

        <div class="step" class:active={currentStep >= 4}>
            <p>
                However, despite recent progress towards long-run cross-country
                convergence, there are still huge differences that have to be
                addressed: in several countries in Sub-Saharan Africa the
                average life expectancy is still less than 60 years, compared to
                more than 80 years in countries in Europe or in Japan.
            </p>
        </div>

        <div class="step" class:active={currentStep >= 5}>
            <HealthTable />
        </div>

        <div class="step" class:active={currentStep >= 6}>
            <h2>The Global Pandemic</h2>

            <p>
                The pandemic is devastating health systems globally and
                threatens health outcomes already achieved. Most countries, in
                particular poor ones, have insufficient health facilities,
                medical supplies and health-care workers to meet the surge in
                demand.
            </p>

            <p>
                By April 2022, the coronavirus causing COVID-19 had infected
                more than 500 million people and killed more than 6.2 million
                worldwide. However, the most recent estimates suggest that the
                global number of excess deaths directly and indirectly
                attributable to COVID-19 could be as high as three times this
                figure.
            </p>
        </div>
    </Scrolly>
</div>
