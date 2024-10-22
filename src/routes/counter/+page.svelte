<script lang="ts">
    import Counter from "$lib/components/counter/Counter.svelte";
</script>


<div class="rounded-lg bg-white p-8 shadow-lg">
    <h1 class="mb-6 text-center text-3xl font-bold text-gray-800">Counters</h1>
    <div class="mx-auto grid grid-cols-3 gap-6 lg:gap-8">
        <Counter/>
        <Counter/>
        <Counter/>
    </div>

</div>
