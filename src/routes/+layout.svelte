<script lang="ts">
    import '../app.css';
    import {Navbar, NavBrand, NavHamburger, NavLi, NavUl} from "flowbite-svelte";

    let {children} = $props();
</script>

<Navbar>
    <NavBrand href="/">
        <img src="/flowbite-svelte-icon-logo.svg" class="me-3 h-6 sm:h-9" alt="Flowbite Logo"/>
        <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">Flowbite</span>
    </NavBrand>
    <NavHamburger/>
    <NavUl>
        <NavLi href="/">Home</NavLi>
        <NavLi href="/counter">Counter</NavLi>
    </NavUl>
</Navbar>

<main class=" mx-auto">
    {@render children()}
</main>

