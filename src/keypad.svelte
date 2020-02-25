<style>
    .container { 
        background-color: #000;
        position:absolute;
        bottom:0;
        display: flex;
        flex-direction: column;
        justify-content:flex-end;
        height:50vh;
        width:100vw;
        transition: transform .3s ease;
    }
    .hidden {
        transform:translateY(50vh)
    }
    .row { 
        display: flex;
        flex-direction: row;
        flex:1;
    }
    .unit {
        position: relative;
        display:flex;
        align-items: center;
        justify-content: center;
        /* background: red; */
        /* flex-shrink:1; */
        height:7vh;
        width:100vw;
        color:white;
    }
    .popup { 
        position:absolute;
        top: 7vh;
        display:flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        flex-wrap: wrap;
        width:100vw;
        color:white;
        background: #000;
        height:calc(50vh - 7vh);
    }
    .unitbutton {
        border:none;
        outline:none;
        background: transparent;
        /* background: blue; */
        color:#aaa;
        width:50vw;
        height: 10vh;
        flex-shrink:0;
        font-size: 3vh;

    }
</style>
<script>
    export let visible = true;
    import {slide} from 'svelte/transition';
    import Key from './key.svelte';
    import { createEventDispatcher } from 'svelte';
    let container;
    let showPopup = false;

    const dispatch = createEventDispatcher();
    function handleTransitionEnd() {
        if (visible)
            dispatch('open');
        else    
            dispatch('close');
    }
</script>
<div bind:this={container} class='container' class:hidden={!visible} on:click on:transitionend={handleTransitionEnd}>
    <div class='unit' data-type='popup' on:click={() => showPopup = !showPopup}>Choose unit ...
    </div>
    {#if showPopup}
        <div class='row' data-type='unit'>
            <Key class='unitbutton' data-type='unit'>black tubs</Key>
            <Key class='unitbutton' data-type='unit'>boxes</Key>
        </div>
        <div class='row' data-type='unit'>
            <Key class='unitbutton' data-type='unit'>trays</Key>
            <Key class='unitbutton' data-type='unit'>bin</Key>
        </div>
        <div class='row' data-type='unit'>
            <Key class='unitbutton' data-type='unit'>shelf</Key>
        </div>
    {:else}
    <div class='row'>
        <Key>1</Key>
        <Key>2</Key>
        <Key>3</Key>
        <Key>1/4</Key>
    </div>
    <div class='row'>
        <Key>4</Key>
        <Key>5</Key>
        <Key>6</Key>
        <Key>1/2</Key>
    </div>
    <div class='row'>
        <Key>7</Key>
        <Key>8</Key>
        <Key>9</Key>
        <Key>3/4</Key>
    </div>
    <div class='row'>
        <Key>+</Key>
        <Key>0</Key>
        <Key>-</Key>
        <Key>X</Key>
    </div>
    {/if}

</div>
