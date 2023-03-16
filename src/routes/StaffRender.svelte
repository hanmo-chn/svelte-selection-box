<script lang="ts">

    export let item: any;
</script>
<div style="position: relative; width: 100%; box-sizing: border-box">
    <div style="position: absolute; right: 8px; top: 4px; font-size: 10px">code:{item.code}</div>
    <div style="padding-top: 20px">
        <span>{item.name}</span>
    </div>
</div>
