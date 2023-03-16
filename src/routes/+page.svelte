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
    ];

    let disable: boolean = true;

    setInterval(()=>{disable = !disable}, 5000)

</script>

<div style="">
    <div style="width: 400px; height: 600px; border: 1px solid #e1e1e1;">
        <SelectionBox {list} disable={disable} itemHeight="80" singleSelect={false} itemRender={StaffRender}>

        </SelectionBox>
    </div>
</div>
