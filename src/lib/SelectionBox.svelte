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
    export let filter: any;
    let className: string = '';
    export {className as class};

    let filteredList = [...list];

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

    let composing:boolean = false;
    let filterText = '';
    let filterValue: string = '';

    const handleInput = (event) => {
        if (composing == false) {
            filterText = filterValue;
        }
    }

    const handleCompositionStart = (event) => {
        event.target.composing = true;
        composing = true;
    }

    const handleCompositionEnd = (event) => {
        event.target.composing = false;
        composing = false;
        filterText = filterValue;
    }

    $: if (disable) {
        filterText = '';
        filterValue = '';
    }

    $: if (filter && filterText && filterText.trim().length > 0) {
        let key = filterText.trim();
        filteredList = list.filter(item=>filter(item, key));
        selectedItems = selectedItems.filter(item=>filteredList.indexOf(item) > -1);
    } else {
        filteredList = [...list];
    }

</script>
<div class="tsui-selection-box {className}"  class:disable {style}>
    {#if filter}
        <div class="selection-box-header">
            <div class="filter-text">
                <input disabled={disable} bind:value={filterValue}
                       on:input={handleInput}
                       on:compositionstart={handleCompositionStart} on:compositionend={handleCompositionEnd}>
            </div>
        </div>
    {/if}
    <div class="selection-box-content">
        {#each filteredList as item}
            <div class="box-item" style="{item$style}{itemHeight > 0 ? `; height: ${itemHeight}px` : ''}"
                 on:click={(e)=>{handleItemClick(item); e.stopPropagation()}}>
                <div class="checkbox-container" class:checked={selectedItems.indexOf(item)>-1}></div>
                <div class="item-content">
                    <svelte:component this={itemRender} {item}/>
                </div>
            </div>
        {/each}
    </div>
</div>
