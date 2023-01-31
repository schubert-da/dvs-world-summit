<script>
    import TableLegend from "./table-legend.svelte";
    import { sdg_health_data } from "../../../../data/sdg_progress_health";

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

    var selected_data = sdg_health_data.slice(0, num_rows);
    var filtered_data = sdg_health_data.slice(0, num_rows);

    console.log(sdg_health_data);

    function filterData(event) {
        
        var key = event.target.value.toUpperCase();
        filtered_data = sdg_health_data.filter((a) => a["Country"].toUpperCase().includes(key));

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

        selected_data = sorted_data.slice(0, num_rows)
    }
</script>

<div class="table-section">
    <h2 class="title">The SGD Index Score Rankings</h2>
    <div class="desc">
        The SDG Index is an assessment of each country's overall performance on the 17 SDGs, giving equal weight to each Goal.
        The score signifies a country's position between the worst possible outcome (score of 0) and the target (score of 100).
        <br><br>
        The following table shows how different countries are working towards achieving their goals in health and well being. Some important definitions in the chart include:
        
        <ul>
            <li>
                <b>Maternal mortality</b> - 
                The estimated number of women, between the age of 15-49, who die from pregnancy-related causes while pregnant or within 42 days of termination of pregnancy, per 100,000 live births.
            </li>
            <li>
                <b>Child Under 5 mortality</b> - 
                The probability that a newborn baby will die before reaching age five, if subject to age-specific mortality rates of the specified year, per 1,000 live births.
            </li>
            <li>
                <b>Life Expectancy</b> - 
                The average number of years that a newborn could expect to live, if he or she were to pass through life exposed to the sex and 
                age-specific death rates prevailing at the time of his or her birth, for a specific year, in a given country, territory, or geographic area.
            </li>
            <li>
                <b>Vaccination</b> - 
                Estimated national routine immunization coverage of infants, expressed as the percentage of surviving infants, 
                children under the age of 12 months, who received two WHO-recommended vaccines. 
            </li>
        </ul>

        <TableLegend />
    </div>

    <h2 class="title">The SGD Index Score Rankings - Health</h2>


    <div class="filter-country">
        <label for="key"> Filter by Country:  </label>
        <input type="text" name="key" id="key" on:input={filterData}/> 
    </div>

    <div class="table">
        <div class="header-label big-label" style="grid-column: 2/4">MATERNAL MORTALITY</div>
        <div class="header-label big-label" style="grid-column: 5/7">CHILD MORTALITY</div>
        <div class="header-label big-label" style="grid-column: 8/10">LIFE EXPECTANCY</div>
        <div class="header-label big-label" style="grid-column: 11/13">VACCINATION</div>
    
        <!-- <div class="header-label country-label sort-by" style="grid-column: 1/1" on:click={() => loadData("Country")}>COUNTRY</div> -->
        <div class="header-label country-label" style="grid-column: 1/1">COUNTRY</div>
    
        <div class="header-label small-label sort-by" style="grid-column: 2/2" on:click={() => loadData("sdg3_matmort_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 3/3">TREND</div>
        <div class="header-label small-label sort-by" style="grid-column: 5/5" on:click={() => loadData("sdg3_u5mort_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 6/6">TREND</div>
        <div class="header-label small-label sort-by" style="grid-column: 8/8" on:click={() => loadData("sdg3_lifee_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 9/9">TREND</div>
        <div class="header-label small-label sort-by" style="grid-column: 11/11" on:click={() => loadData("sdg3_vac_score")}>INDEX SCORE</div>
        <div class="header-label small-label" style="grid-column: 12/12">TREND</div>
       
    
        {#each selected_data as country, index}
            <div
                class="data-country-name"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 1/1;"}>
                {country.Country} <br />
                <!-- <span>SDG Index rank: {country["2022 SDG Index Rank"]}</span> -->
            </div>
    
    
            <!-- SDG3 MATERNAL MORTALITY -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 2/2; background-color: "+ color_map_score[country["sdg3_matmort_color"]]}>
                    {country["sdg3_matmort_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 3/3; background-color: "+color_map_trend[country['sdg3_matmort_trend']]}>
                    {value_map_trend[country["sdg3_matmort_trend"]]}
            </div>
    
            <div class="data-divider"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 4/4;"}>
            </div>
    
    
            <!-- SDG3 CHILD UNDER 5 MORTALITY -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 5/5; background-color: "+ color_map_score[country["sdg3_u5mort_color"]]}>
                {country["sdg3_u5mort_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 6/6; background-color: "+color_map_trend[country['sdg3_matmort_trend']]}>
                {value_map_trend[country["sdg3_matmort_trend"]]}
            </div>
    
            <div class="data-divider"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 7/7;"}>
            </div>
    
    
            <!-- SDG3 LIFE EXPECTANCY -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 8/8; background-color: "+ color_map_score[country["sdg3_lifee_color"]]}>
                {country["sdg3_lifee_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 9/9; background-color: "+color_map_trend[country['sdg3_lifee_trend']]}>
                {value_map_trend[country["sdg3_lifee_trend"]]}
            </div>
    
            <div class="data-divider"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 10/10;"}>
            </div>
    
    
            <!-- SDG3 VACCINATION METRIC -->
            <div
                class="data-index-score"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 11/11; background-color: "+ color_map_score[country["sdg3_vac_color"]]}>
                {country["sdg3_vac_score"]}
            </div>
    
            <div
                class="data-index-trend"
                style={"grid-row:" + (index+3) + "/" + (index+3) + "; grid-column: 12/12; background-color: "+color_map_trend[country['sdg3_vac_trend']]}>
                {value_map_trend[country["sdg3_vac_trend"]]}
            </div>
        {/each}
    </div>
</div>


<style>
    .table-section {
        width: fit-content;
        margin: 0 auto;
    }

    .title, .desc{
        width: fit-content;
        margin: 0 auto;
        color: #222;
    }

    .desc {
        font-size: 18px;
        width: 60ch;
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
</style>
