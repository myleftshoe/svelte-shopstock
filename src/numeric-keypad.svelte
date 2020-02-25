
<script>
    import KeyRow from './keyrow.svelte';
    import Key from './key.svelte';
    const type = 'numeric'
</script>
<KeyRow>
    <Key {type}>1</Key>
    <Key {type}>2</Key>
    <Key {type}>3</Key>
    <Key {type}>1/4</Key>
</KeyRow>
<KeyRow>
    <Key {type}>4</Key>
    <Key {type}>5</Key>
    <Key {type}>6</Key>
    <Key {type}>1/2</Key>
</KeyRow>
<KeyRow>
    <Key {type}>7</Key>
    <Key {type}>8</Key>
    <Key {type}>9</Key>
    <Key {type}>3/4</Key>
</KeyRow>
<KeyRow>
    <Key {type}>+</Key>
    <Key {type}>0</Key>
    <Key {type}>-</Key>
    <Key {type}>X</Key>
</KeyRow>
