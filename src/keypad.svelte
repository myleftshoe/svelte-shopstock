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
<script context='module'>
	export const KEYPAD_TYPE = {
        NUMERIC: 'numeric',
        UNIT: 'unit'
	}
</script>
<script>
    export let visible = true;
    import NumericKeypad from './numeric-keypad.svelte';
    import UnitKeypad from './unit-keypad.svelte';
    import { createEventDispatcher } from 'svelte';
    export let type = 'numeric';
    let container;
    
    const dispatch = createEventDispatcher();
    function handleTransitionEnd() {
        if (visible)
            dispatch('open');
        else    
            dispatch('close');
    }
    function toggleType() {
        if (type === KEYPAD_TYPE.NUMERIC)
            type = KEYPAD_TYPE.UNIT;
        else
            type = KEYPAD_TYPE.NUMERIC;
    }
</script>
<div bind:this={container} class='container' class:hidden={!visible} on:click on:transitionend={handleTransitionEnd}>
    <div class='unit' data-type='popup' on:click={toggleType}>Choose unit ...</div>
    {#if type === 'numeric'}
        <NumericKeypad/>
    {:else}
        <UnitKeypad/>
    {/if}
</div>
