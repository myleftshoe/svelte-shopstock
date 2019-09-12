<style>
    button {
        background-color: #333;
        border: 2px solid black;
        outline:none;
        cursor: pointer;
        color:white;
        font-size:4vh;
        align-content:flex-start;
        flex:1;
    }
    button:active {
        background-color: #777;
    }
</style>
<button on:click>
    <slot/>
</button>
