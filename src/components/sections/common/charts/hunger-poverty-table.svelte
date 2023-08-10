<script>
    import TableLegend from "./table-legend.svelte";
    import { sdg_hunger_poverty_data } from "../../../../data/sdg_progress_hunger_poverty";

    var num_rows = 15;
    var color_map_score = {
        "green": "#509E50",
        "yellow": "#FFA531",
        "orange": "#E17B4F",
        "red": "#DB2A4A",
        "grey": "#CCC",
        "": "#CCC"
    }

    var color_map_trend = {
        "↑": "#509E50",
        "➚": "#FFA531",
        "→": "#E17B4F",
        "↓": "#DB2A4A",
        "": "#CCC"
    }

    var value_map_trend = {
        "↑": "▲",
        "➚": "◀",
        "→": "▶",
        "↓": "▼",
        "": ""
    }

    var sort_ascending = true;

    var selected_data = sdg_hunger_poverty_data.slice(0, num_rows);
    var filtered_data = sdg_hunger_poverty_data.slice(0, num_rows);

    console.log(sdg_hunger_poverty_data);

    function filterData(event) {
        
        var key = event.target.value.toUpperCase();
        filtered_data = sdg_hunger_poverty_data.filter((a) => a["Country"].toUpperCase().includes(key));

        selected_data = filtered_data.slice(0, num_rows);
    }

    function loadData(column) {
        var sorted_data;
        
        filtered_data = filtered_data.filter((a) => a[column] !== "");

        if(sort_ascending) {
            sort_ascending = false;
            sorted_data = filtered_data.sort( (a,b) => b[column] - a[column] );
        }
        else {
            sort_ascending = true;
            sorted_data = filtered_data.sort( (a,b) => a[column] - b[column] );
        }

        // console.log(sorted_data);
        selected_data = sorted_data.slice(0, num_rows)
        console.log(selected_data);
    }
</script>

<div class="table-section">
    <h2 class="title">The SGD Index Score Rankings</h2>
    <div class="desc">
        The SDG Index is an assessment of each country's overall performance on the 17 SDGs, giving equal weight to each Goal.
        The score signifies a country's position between the worst possible outcome (score of 0) and the target (score of 100).
        <br><br>
        The following table shows how different countries are working towards achieving their goals in the areas of poverty eradication 
        and eliminating hunger. Some important definitions in the chart include:
        
        <ul>
            <li>
                <b>Poverty headcount ratio</b> - 
                The poverty headcount ratio at $1.90/day refers to the proportion of the population that lives below the poverty line defined as $1.90/day.
                This poverty line is set by the World Bank and is used as an anchor to measure absolute poverty.
            </li>
            <li>
                <b>Undernourishment</b> - 
                The percentage of the population whose food intake is insufficient to meet dietary energy requirements for a minimum of one year. 
                Dietary energy requirements are defined as the amount of dietary energy required by an individual to maintain body functions, health and normal activity as determined by the FAO.
            </li>
            <li>
                <b>Stunting</b> - 
                Children who are stunted are determined as having a height which falls two standard deviations below the median height-for-age 
                of the World Health Organization's Child Growth Standards. Stunting is an indicator of severe malnutrition.
            </li>
            <li>
                <b>Wasting</b> - 
                The percentage of children up to the age of 5 years whose weight falls below minus two standard deviations from the median weight for their age, 
                according to the WHO Child Growth Standards.
            </li>
        </ul>

        <TableLegend />

        <h2 class="title">The SGD Index Score Rankings - Hunger and Poverty</h2>
    
    
        <div class="filter-country">
            <label for="key"> Filter by Country:  </label>
            <input type="text" name="key" id="key" on:input={filterData}/> 
        </div>
    </div>

    <div class="table">
        <div class="header-label big-label" style="grid-column: 2/4">POVERTY HEADCOUNT</div>
        <div class="header-label big-label" style="grid-column: 5/7">UNDERNOURISHMENT</div>
        <div class="header-label big-label" style="grid-column: 8/10">STUNTING</div>
        <div class="header-label big-label" style="grid-column: 11/13">WASTING</div>
    
        <!-- <div class="header-label country-label sort-by" style="grid-column: 1/1" on:click={() => loadData("Country")}>COUNTRY</div> -->
        <div class="header-label country-label" style="grid-column: 1/1">COUNTRY</div>
    
        <div class="header-label small-label sort-by" style="grid-column: 2/2" on:click={() => loadData("sdg1_wpc_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 3/3">TREND</div>
        <div class="header-label small-label sort-by" style="grid-column: 5/5" on:click={() => loadData("sdg2_undernsh_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 6/6">TREND</div>
        <div class="header-label small-label sort-by" style="grid-column: 8/8" on:click={() => loadData("sdg2_stunting_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 9/9">TREND</div>
        <div class="header-label small-label sort-by" style="grid-column: 11/11" on:click={() => loadData("sdg2_wasting_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 12/12">TREND</div>
       
    
        {#each selected_data as country, index}
            <div
                class="data-country-name"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 1/1;"}>
                {country.Country} <br />
                <!-- <span>SDG Index rank: {country["2022 SDG Index Rank"]}</span> -->
            </div>
    
    
            <!-- SDG1 POVERTY METRIC -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 2/2; background-color: "+ color_map_score[country["sdg1_wpc_color"]]}>
                    {country["sdg1_wpc_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 3/3; background-color: "+color_map_trend[country['sdg1_wpc_trend']]}>
                    {value_map_trend[country["sdg1_wpc_trend"]]}
            </div>
    
            <div class="data-divider"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 4/4;"}>
            </div>
    
    
            <!-- SDG2 UNDERNOURISHMENT -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 5/5; background-color: "+ color_map_score[country["sdg2_undernsh_color"]]}>
                {country["sdg2_undernsh_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 6/6; background-color: "+color_map_trend[country['sdg2_undernsh_trend']]}>
                {value_map_trend[country["sdg2_undernsh_trend"]]}
            </div>
    
            <div class="data-divider"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 7/7;"}>
            </div>
    
    
            <!-- SDG2 STUNTING -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 8/8; background-color: "+ color_map_score[country["sdg2_stunting_color"]]}>
                {country["sdg2_stunting_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 9/9; background-color: "+color_map_trend[country['sdg2_stunting_trend']]}>
                {value_map_trend[country["sdg2_stunting_trend"]]}
            </div>
    
            <div class="data-divider"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 10/10;"}>
            </div>
    
    
            <!-- SDG2 WASTING -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 11/11; background-color: "+ color_map_score[country["sdg2_wasting_color"]]}>
                {country["sdg2_wasting_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 12/12; background-color: "+color_map_trend[country['sdg2_wasting_trend']]}>
                {value_map_trend[country["sdg2_wasting_trend"]]}
            </div>
        {/each}
    </div>
</div>


<style>
    .table-section {
        margin: 0 auto;
    }

    .title, .desc{
        width: fit-content;
        margin: 0 auto;
        color: #222;
    }

    .desc {
        font-size: 18px;
        max-width: 60ch;
        margin-top: 20px;
    }


    .desc li:first-of-type{
        margin-top: 30px;
    }
    .desc li{
        color: #444;
        margin-top: 15px;
        font-size: 17px;
    }

    .filter-country{
        margin: 25px 0 20px 0;

    }

    .filter-country label{
        font-size: 18px;
        text-transform: uppercase;
        color: #666;
        letter-spacing: -0.4px;
        margin-right: 10px;
    }
    
    .table {
        margin: 0 auto;
        width: 900px;

        display: grid;
        grid-template-columns: 150px repeat(4, 120px 60px 12px);
        grid-template-rows: repeat(17, 50px);

        row-gap: 0px;
    }

    .table div{
        border-bottom: 4px solid #efefef;
    }

    .header-label{
        grid-row: 2/2;
        text-align: left;
        padding: 5px;
        transition: background-color 0.2s ease-in;
    }

    .header-label:hover{
        background-color: #ccc;
    }
    

    .country-label {
        text-align: left;
        text-transform: uppercase;
        color: #222;
        font-weight: bold;
        grid-column: 1/1;
        grid-row: 2/2;
    }

    .header-label.small-label{
        color: #444;
        padding-top: 6px;
    }

    .header-label.big-label{
        color: #222;
        font-weight: bold;
        text-align: center;
        grid-row: 1/1;
        border-bottom: 2px solid #999;
    }

    .data-country-name{
        display: flex;
        flex-direction: column;
        font-size: 20px;
        justify-content: center;
        align-items:  flex-start;
    }

    .data-index-score{ 
        font-size: 20px;
        color: #222;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .data-index-trend{ 
        color: #efefef;
        font-size: 18px;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content: center;

        border-left: 2px solid #efefef;
        /* border-right: 2px solid #222; */
    }

    .table .data-divider{
        background-color: #222; 
        border-bottom: none;
        border-left: 4px solid #efefef;
        border-right: 4px solid #efefef;
    }

    /* Sort CSS */
    .header-label.sort-by.sort-by { 
        padding-right: 18px;
        position: relative;
    }
    .header-label.sort-by:before,
    .header-label.sort-by:after {
        border: 4px solid transparent;
        content: "";
        display: block;
        height: 0;
        right: 5px;
        top: 75%;
        position: absolute;
        width: 0;
    }

    .header-label.sort-by:before {
        border-bottom-color: #666;
        margin-top: -9px;
    }
    
    .header-label.sort-by:after {
        border-top-color: #666;
        margin-top: 1px;
    }

    @media (max-width: 720px) {

        .table {
            overflow-x: scroll;
            grid-template-columns: 100px repeat(4, 10fr 5fr 1fr);
            grid-template-rows: repeat(17, 40px);
            font-size: 16px;
        }

        .data-country-name, .big-label, .header-label.big-label{
            font-size: 16px;
        }
        
        .header-label.big-label{
            color: #222;
            font-weight: bold;
            text-align: center;
            grid-row: 1/1;
            border-bottom: 2px solid #999;
        }
    }
</style>
