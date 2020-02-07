<script>
    export let src;
    export let classes;

    const svg = src.replace('<svg', '<svg class="' + classes + '"');
</script>

{@html svg}