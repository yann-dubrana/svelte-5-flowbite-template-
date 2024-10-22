<script>
    import ProductTable from "$lib/components/products/Table.svelte";
    import {Modal} from "flowbite-svelte";
    import ProductForm from "$lib/components/products/Form.svelte";

    let open = $state(false)

</script>

<Modal title="Add a new product" bind:open autoclose>
    <ProductForm/>
</Modal>
<ProductTable bind:openForm={open}/>