<script>
    export let sourceIndex = 0;
    export let sourceDescription = "Trust me bro - Me, 1997";
</script>

<div class="source-container">
    <div class="source-index">
        <div class="source-number">
            {sourceIndex}
        </div>
    </div>
    <div class="source-description">
        {sourceDescription}
    </div>
</div>

<style>
    :root {
        --annotation-height: 30px;
    }

    .source-container {
        position: relative;
        color: #444;
        font-size: 16px;
        height: var(--annotation-height);
        width: fit-content;
        line-height: 1.4;
        letter-spacing: -0.4px;

        display: flex;
        flex-direction: row;
        align-items: center;

        border: 1px solid #666;
        border-left: none;
        border-right: none;

        margin: 0px 0 70px 0;
    }

    .source-container::after, .source-container::before{
        position: absolute;
        content: "";
        width: calc( var( --annotation-height) / 2);
        height: var( --annotation-height);
        border: 1px solid #666;
    }

    .source-container::after {
        border-left: none;
        border-top-right-radius: calc( var( --annotation-height) / 2);
        border-bottom-right-radius: calc( var( --annotation-height) / 2);

        top: -1px;
        right: -12px;
    }

    .source-container::before {
        border-right: none;
        border-top-left-radius: calc( var( --annotation-height) / 2);
        border-bottom-left-radius: calc( var( --annotation-height) / 2);

        top: -1px;
        left: -12px;
    }

    .source-index {
        color: #efefef;
        font-size: 16px;
        background-color: #444;
        border-radius: 50%;
        width: 25px;
        height: 25px;

        display: flex;
        justify-content: center;
        align-items: center;
        margin-right: 10px;
        margin-left: -8px;
    }


    

</style>