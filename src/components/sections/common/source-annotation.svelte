<div class="source-container">
    <div class="source-index">
        <div class="source-number">
            2
        </div>
    </div>
    <div class="source-description">
        This is a long source.. will figure out what goes here eventually.
    </div>
</div>

<style>
    :root {
        --annotation-height: 30px;
    }

    .source-container {
        position: relative;
        color: #444;
        font-size: 18px;
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