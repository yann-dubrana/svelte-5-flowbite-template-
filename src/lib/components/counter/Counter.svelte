<script lang="ts">
    import {Button, Card} from "flowbite-svelte";

    class Counter {
        value: number = $state(0);

        increment() {
            this.value++;
        }

        decrement() {
            this.value--;
        }

        double() {
            this.value *= 2;
        }
    }

    let count = new Counter();
</script>
<Card>
    <div class="mb-6 text-center text-6xl font-bold text-blue-600">
        {count.value}
    </div>

    <div class="flex gap-4 justify-center">
        <Button
                onclick={()=>{count.decrement()}}
                class="rounded-full bg-red-500 px-6 py-2 text-white hover:bg-red-600 transition-colors"
        >
            -
        </Button>

        <Button
                onclick={()=>{count.increment()}}
                class="rounded-full bg-green-500 px-6 py-2 text-white hover:bg-green-600 transition-colors"
        >
            +
        </Button>

        <Button
                onclick={()=>{count.double()}}
                class="rounded-full bg-purple-500 px-6 py-2 text-white hover:bg-purple-600 transition-colors"
        >
            **
        </Button>
    </div>
</Card>