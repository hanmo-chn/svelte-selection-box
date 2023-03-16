<script lang="ts">

    import {SvelteComponent} from "svelte";
    import "@ticatec/enhanced-utils";

    export let list: Array<any>;
    export let style: string = '';
    export let item$style: string = '';
    export let singleSelect: boolean = false;
    export let itemRender: SvelteComponent;
    export let itemHeight: number = 0;
    export let selectedItems: Array<any> = [];
    export let disable: boolean = false;
    export let readonly: boolean = false;

    let className: string = '';
    export {className as class};

    const handleItemClick = (item) => {
        if (!disable && !readonly) {
            if (singleSelect) {
                selectedItems = [item];
            } else {
                if (selectedItems.indexOf(item) > -1) {
                    selectedItems = selectedItems.filter((el) => el !== item);
                } else {
                    selectedItems = [...selectedItems, item];
                }
            }
        }
    }

</script>
<div class="tsui-selection-box {className}"  class:disable {style}>
    {#each list as item}
        <div class="box-item" style="{item$style}{itemHeight > 0 ? `; height: ${itemHeight}px` : ''}"
             on:click={(e)=>{handleItemClick(item); e.stopPropagation()}}>
            <div class="checkbox-container" class:checked={selectedItems.indexOf(item)>-1}></div>
            <div class="item-content">
                <svelte:component this={itemRender} {item}/>
            </div>
        </div>
    {/each}
</div>
