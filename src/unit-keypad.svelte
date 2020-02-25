<script>
    import KeyRow from './keyrow.svelte';
    import Key from './key.svelte';
    const type = 'unit';
</script>
<KeyRow>
    <Key {type}>bags</Key>
    <Key {type}>black tubs</Key>
</KeyRow>
<KeyRow>
    <Key {type}>boxes</Key>
    <Key {type}>trays</Key>
</KeyRow>
<KeyRow>
    <Key {type}>bin</Key>
    <Key {type}>shelf</Key>
</KeyRow>
