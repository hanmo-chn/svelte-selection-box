<script lang="ts">

    import SelectionBox from "../lib/SelectionBox.svelte";
    import StaffRender from "./StaffRender.svelte";
    import "../lib/tsui-selection-box.scss"

    let list = [
        {code: "10114568", name: "张三"},
        {code: "12114568", name: "张三峰"},
        {code: "13114568", name: "张四峰"},
        {code: "14114568", name: "张无峰"},
        {code: "15114568", name: "张六峰"},
        {code: "16114568", name: "张琪峰"},
        {code: "20114568", name: "张三2"},
        {code: "22114568", name: "张三峰2"},
        {code: "23114568", name: "张四峰2"},
        {code: "24114568", name: "张无峰2"},
        {code: "25114568", name: "张六峰2"},
        {code: "26114568", name: "张琪峰2"}
    ];

    let disable: boolean = false;

    let filter = (user, text) => user.name.includes(text);

</script>

<div style="">
    <div style="width: 400px; height: 600px; border: 1px solid #333333;">
        <SelectionBox {list} disable={disable} {filter} itemHeight="80" singleSelect={false} itemRender={StaffRender}>

        </SelectionBox>
    </div>
</div>
