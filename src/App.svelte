<script>
    import Header from './components/Header.svelte';
    import Sidebar from './components/Sidebar.svelte';
    import {quickSort} from './sorts/quickSort.js';
    import {onMount} from 'svelte';

    export let sortType = 'quick';
    let size = 50;
    let width = 0;
    let height = 0;
    let dataset = [];
    let columnWidth = 0;
    let padding = 30;

    onMount(() => {
        columnWidth = (width - padding - size) / size;
        handleGenerateDataset(size, height - padding);
    });

    function handleGenerateDataset(size, range) {
        let arr = [];
        for (let i = 0; i < size; i++) {
            arr.push({id: i, value: Math.floor((Math.random() * Math.floor(range)) + 1)});
        }

        dataset = arr;
    }

    function handleSortType(type) {
        sortType = type.detail.type;
    }

    function handleStart() {
        switch (sortType) {
            case 'quick':
                dataset = quickSort(dataset, 0, dataset.length - 1);
                break;
            case 'select':
                console.log('select sort');
                break;
            case 'bubble':
                console.log('bubble sort');
                break;
        }
    }
</script>

<Header on:start={() => handleStart()}/>
<main class="ssv-main">
    <Sidebar {sortType} on:sortType={(type) => handleSortType(type)}
             on:generate={() => handleGenerateDataset(size, height - padding)}/>

    <div class="ssv-chart"
         bind:clientWidth={width}
         bind:clientHeight={height}
         style={`padding: ${padding/2}px;`}>

        {#each dataset as arr}
            <span style="{`width: ${columnWidth}px; height: ${arr.value}px`}"></span>
        {/each}

    </div>
</main>

<style lang="scss" global>
    @import "./styles/global.scss";

    .ssv-main {
        display: flex;
        background-color: $c-light-blue;
    }

    .ssv-chart {
        display: flex;
        width: calc(85% - 40px);
        border-radius: 5px;
        background-color: $c-basic;
        margin: 15px 20px;

        span {
            display: block;
            width: 20px;
            background-color: $c-tertiary;
            margin: auto 1px 0;
        }
    }
</style>