<style>
    .container { 
        background-color: #f003;
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
</style>
<script>
    export let visible = true;
    import Key from './key.svelte';
    import { createEventDispatcher } from 'svelte';
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
</div>
