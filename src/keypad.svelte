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
</style>
<script>
    export let visible = true;
    import NumericKeypad from './numeric-keypad.svelte';
    import UnitKeypad from './unit-keypad.svelte';
    import { createEventDispatcher } from 'svelte';
    export let numeric = true;
    let container;
    
    const dispatch = createEventDispatcher();
    function handleTransitionEnd() {
        if (visible)
            dispatch('open');
        else    
            dispatch('close');
    }
</script>
<div bind:this={container} class='container' class:hidden={!visible} on:click on:transitionend={handleTransitionEnd}>
    <div class='unit' data-type='popup' on:click={() => numeric = !numeric}>Choose unit ...</div>
    {#if numeric}
        <NumericKeypad/>
    {:else}
        <UnitKeypad/>
    {/if}
</div>
