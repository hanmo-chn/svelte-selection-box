<script lang="ts">

    import {SvelteComponent} from "svelte";
    import "@ticatec/enhanced-utils";

    export let list: Array<any>;
    export let singleSelect: boolean = false;
    export let itemRender: SvelteComponent;

    let selectedItems = [];

    const handleItemClick = (item) => {
        if (singleSelect) {
            selectedItems = [item];
        } else {
            if (selectedItems.indexOf(item) > -1) {
                selectedItems.remove(item);
            } else {
                selectedItems.push(item);
            }
            selectedItems = [...selectedItems]
        }
    }

</script>
<div class="tsui-selection-box">
    {#each list as item}
        <div class="box-item" on:click={(e)=>{handleItemClick(item); e.stopPropagation();}}>
            <input type="checkbox" on:click={(e)=>{e.preventDefault()}} checked={selectedItems.indexOf(item)>-1}>
            <svelte:component this={itemRender} {item}/>
        </div>
    {/each}
</div>