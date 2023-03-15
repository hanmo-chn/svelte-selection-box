<script lang="ts">

    import SelectionBox from "../lib/SelectionBox.svelte";
    import StaffRender from "./StaffRender.svelte";
    import "../lib/tsui-selection-box.scss"

    let list = [
        {code: "11111", name: "James"},
        {code: "11112", name: "Jason"},
        {code: "11113", name: "Peter"},
        {code: "11114", name: "Ben"},
        {code: "11115", name: "Ada"},
        {code: "11116", name: "Toby"}
    ]

</script>

<div style="">
    <div style="width: 400px; height: 120px; border: 1px solid #e1e1e1;">
        <SelectionBox {list} singleSelect={false} itemRender={StaffRender}>

        </SelectionBox>
    </div>
</div>
