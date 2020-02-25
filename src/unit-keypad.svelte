<script>
    import KeyRow from './keyrow.svelte';
    import Key from './key.svelte';
    const type = 'unit';
</script>
<KeyRow>
    <Key {type}>black tubs</Key>
    <Key {type}>boxes</Key>
</KeyRow>
<KeyRow>
    <Key {type}>trays</Key>
    <Key {type}>bin</Key>
</KeyRow>
<KeyRow>
    <Key {type}>shelf</Key>
</KeyRow>
