<script>
    import UndernutritionBarChart from "./charts/undernutrition-bar-chart.svelte";
    import FoodInsecurityAreaChart from "./charts/food-insecurity-area-chart.svelte";
    import Scrolly from "../common/utils/scrolly.svelte";

    let currentStep;
</script>

<div class="section poverty-section">
    <Scrolly bind:value={currentStep}>
        <div class="step" class:active={currentStep >= 0}>
            <h1>Eradicating Hunger</h1>
            <p>
                Having a diet which is both sufficient in terms of energy
                (caloric) requirements and diverse to meet additional
                nutritional needs is essential for good health. The UN has set a
                global target as part of the Sustainable Development Goals to
                "end hunger by 2030". Currently we are far from reaching this
                target.
            </p>
        </div>

        <div class="step" class:active={currentStep >= 1}>
            <br />
            <UndernutritionBarChart />
        </div>

        <div class="step" class:active={currentStep >= 2}>
            <h3 class="para-header" style="margin-left: 22px;">
                Why is hunger and food insecurity getting worse?
            </h3>

            <p>
                Public investment in agriculture globally is declining, small
                scale food producers and family farmers require much greater
                support and increased investment in infrastructure and
                technology for sustainable agriculture is urgently needed. 
                A fundamental shift in trajectory is needed to achieve the
                2030 nutrition targets.
            </p>

            <p>
                An estimated 821 million people -
                <span class="highlight">
                    approximately 1 in 9 people in the world were undernourished
                    in 2017
                </span>
                up from 784 million in 2015. Data also shows how this statistic is
                worse in developing countries.
            </p>
        </div>

        <div
            class="step"
            class:active={currentStep >= 3}
            style="margin-bottom: 60px;"
        >
            <FoodInsecurityAreaChart />
        </div>

        <div class="step" class:active={currentStep >= 4}>
            <p>
                Between 2014 and the onset of the pandemic, the number of people
                going hungry and suffering from food insecurity had been
                gradually rising. The COVID-19 crisis has pushed those rising
                rates even higher. The war in Ukraine is further disrupting
                global food supply chains leading to widespread hunger issues.
            </p>
            <p>
                Between 83 and 132 million more people may already have been
                pushed into chronic hunger in 2020.
            </p>
            <br />
        </div>
    </Scrolly>
</div>
