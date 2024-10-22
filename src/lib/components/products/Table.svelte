<script lang="ts">

    import {onMount} from 'svelte';

    import {
        TableBody,
        TableBodyCell,
        TableBodyRow,
        TableHead,
        TableHeadCell,
        TableSearch,
        Button,
        Dropdown,
        DropdownItem,
        Checkbox,
        ButtonGroup
    } from 'flowbite-svelte';

    import {Section} from 'flowbite-svelte-blocks';

    import {
        PlusOutline,
        ChevronDownOutline,
        FilterSolid,
        ChevronRightOutline,
        ChevronLeftOutline
    } from 'flowbite-svelte-icons';

    interface Product {
        id: number;
        title: string;
        description: string;
        price: number;
        discountPercentage: number;
        rating: number;
        stock: number;
        brand: string;
        category: string;
        thumbnail: string;
        images: string[];
    }

    interface ProductListResponse {
        products: Product[];
        total: number;
        skip: number;
        limit: number;
    }


    interface Props {
        openForm: boolean;
    }

    let {openForm = $bindable()}: Props = $props()

    let divClass: string = 'bg-white dark:bg-gray-800 relative shadow-md sm:rounded-lg overflow-hidden';
    let innerDivClass: string = 'flex flex-col md:flex-row items-center justify-between space-y-3 md:space-y-0 md:space-x-4 p-4';
    let searchClass: string = 'w-full md:w-1/2 relative';
    let classInput: string = "text-gray-900 text-sm rounded-lg focus:ring-primary-500 focus:border-primary-500 block w-full p-2  pl-10";

    let searchTerm: string = $state('');

    let currentPosition: number = $state(0);
    const itemsPerPage: number = 10;
    const showPage: number = 5;
    let paginationData: Product[] = $state([])
    let totalPages: number = $derived(Math.ceil(paginationData.length / itemsPerPage));
    let totalItems: number = $derived(paginationData.length);
    let currentPage: number = $derived(Math.ceil((currentPosition + 1) / itemsPerPage))

    let startPage: number = $derived(Math.max(1, currentPage - Math.floor(showPage / 2)));
    let endPage: number = $derived(Math.min(startPage + showPage - 1, totalPages));
    let pagesToShow: number[] = $derived(Array.from({length: endPage - startPage + 1}, (_, i) => startPage + i));


    let startRange: number = $derived(currentPosition + 1);
    let endRange: number = $derived(Math.min(currentPosition + itemsPerPage, totalItems))

    let currentPageItems = $derived(paginationData.slice(currentPosition, currentPosition + itemsPerPage))
    let filteredItems = $derived(paginationData.filter((item) => item.title.toLowerCase().indexOf(searchTerm.toLowerCase()) !== -1))

    onMount(async () => {
        let response = await fetch('https://dummyjson.com/products?limit=100')
        let data: ProductListResponse = await response.json()
        paginationData = data.products;
    })

    const loadNextPage = () => {
        if (currentPosition + itemsPerPage < paginationData.length) {
            currentPosition += itemsPerPage;
        }
    }

    const loadPreviousPage = () => {
        if (currentPosition - itemsPerPage >= 0) {
            currentPosition -= itemsPerPage;
        }
    }


    const goToPage = (pageNumber) => {
        currentPosition = (pageNumber - 1) * itemsPerPage;
    }

</script>

<Section name="advancedTable" classSection='bg-gray-50 dark:bg-gray-900 p-3 sm:p-5'>
    <TableSearch placeholder="Search" hoverable={true} bind:inputValue={searchTerm} {divClass} {innerDivClass}
                 {searchClass} {classInput}>

        <div slot="header"
             class="w-full md:w-auto flex flex-col md:flex-row space-y-2 md:space-y-0 items-stretch md:items-center justify-end md:space-x-3 flex-shrink-0">
            <Button onclick={() => {openForm = true}}>
                <PlusOutline class="h-3.5 w-3.5 mr-2"/>
                Add product
            </Button>
            <Button color='alternative'>Actions
                <ChevronDownOutline class="w-3 h-3 ml-2 "/>
            </Button>
            <Dropdown class="w-44 divide-y divide-gray-100">
                <DropdownItem>Mass Edit</DropdownItem>
                <DropdownItem>Delete all</DropdownItem>
            </Dropdown>
            <Button color='alternative'>Filter
                <FilterSolid class="w-3 h-3 ml-2 "/>
            </Button>
            <Dropdown class="w-48 p-3 space-y-2 text-sm">
                <h6 class="mb-3 text-sm font-medium text-gray-900 dark:text-white">Choose brand</h6>
                <li>
                    <Checkbox>Apple (56)</Checkbox>
                </li>
                <li>
                    <Checkbox>Microsoft (16)</Checkbox>
                </li>
                <li>
                    <Checkbox>Razor (49)</Checkbox>
                </li>
                <li>
                    <Checkbox>Nikon (12)</Checkbox>
                </li>
                <li>
                    <Checkbox>BenQ (74)</Checkbox>
                </li>
            </Dropdown>
        </div>
        <TableHead>
            <TableHeadCell padding="px-4 py-3" scope="col">Product name</TableHeadCell>
            <TableHeadCell padding="px-4 py-3" scope="col">Brand</TableHeadCell>
            <TableHeadCell padding="px-4 py-3" scope="col">Category</TableHeadCell>
            <TableHeadCell padding="px-4 py-3" scope="col">Price</TableHeadCell>
        </TableHead>
        <TableBody class="divide-y">
            {#if searchTerm !== ''}
                {#each filteredItems as item (item.id)}
                    <TableBodyRow>
                        <TableBodyCell tdClass="px-4 py-3">{item.title}</TableBodyCell>
                        <TableBodyCell tdClass="px-4 py-3">{item.brand}</TableBodyCell>
                        <TableBodyCell tdClass="px-4 py-3">{item.category}</TableBodyCell>
                        <TableBodyCell tdClass="px-4 py-3">{item.price}</TableBodyCell>
                    </TableBodyRow>
                {/each}
            {:else}
                {#each currentPageItems as item (item.id)}
                    <TableBodyRow>
                        <TableBodyCell tdClass="px-4 py-3">{item.title}</TableBodyCell>
                        <TableBodyCell tdClass="px-4 py-3">{item.brand}</TableBodyCell>
                        <TableBodyCell tdClass="px-4 py-3">{item.category}</TableBodyCell>
                        <TableBodyCell tdClass="px-4 py-3">{item.price}</TableBodyCell>
                    </TableBodyRow>
                {/each}
            {/if}
        </TableBody>
        <div slot="footer"
             class="flex flex-col md:flex-row justify-between items-start md:items-center space-y-3 md:space-y-0 p-4"
             aria-label="Table navigation">
      <span class="text-sm font-normal text-gray-500 dark:text-gray-400">
        Showing
        <span class="font-semibold text-gray-900 dark:text-white">{startRange}-{endRange}</span>
        of
        <span class="font-semibold text-gray-900 dark:text-white">{totalItems}</span>
      </span>
            <ButtonGroup>
                <Button on:click={loadPreviousPage} disabled={currentPosition === 0}>
                    <ChevronLeftOutline size='xs' class='m-1.5'/>
                </Button>
                {#each pagesToShow as pageNumber}
                    <Button on:click={() => goToPage(pageNumber)}>{pageNumber}</Button>
                {/each}
                <Button on:click={loadNextPage} disabled={ totalPages === endPage }>
                    <ChevronRightOutline size='xs' class='m-1.5'/>
                </Button>
            </ButtonGroup>
        </div>
    </TableSearch>
</Section>