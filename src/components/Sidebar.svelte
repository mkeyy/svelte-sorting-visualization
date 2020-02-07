<script>
    import {createEventDispatcher} from 'svelte';
    import AssetSVG from './AssetSVG.svelte';
    import icQuick from '../../public/img/icons/ic-quick.svg';
    import icSelect from '../../public/img/icons/ic-select.svg';
    import icBubble from '../../public/img/icons/ic-bubble.svg';

    export let sortType;
    const dispatch = createEventDispatcher();

    function handleSortSelect(type) {
        sortType = type;
        dispatch('sortType', {type: sortType});
    }
</script>

<aside class="ssv-sidebar">
    <div class="ssv-sorts">
        <span class="ssv-h4">Types</span>
        <ul class="ssv-list--unstyled ssv-menu">
            <li class="ssv-menu__item{sortType === 'quick' ? ' ssv-active' : ''}" on:click={()=> handleSortSelect('quick')}>
                <AssetSVG src={icQuick} classes="ssv-svg--inline ssv-svg--ic-quick"/>
                <span>Quick Sort</span>
            </li>
            <li class="ssv-menu__item{sortType === 'select' ? ' ssv-active' : ''}" on:click={()=> handleSortSelect('select')}>
                <AssetSVG src={icSelect} classes="ssv-svg--inline ssv-svg--ic-select"/>
                <span>Select Sort</span>
            </li>
            <li class="ssv-menu__item{sortType === 'bubble' ? ' ssv-active' : ''}" on:click={()=> handleSortSelect('bubble')}>
                <AssetSVG src={icBubble} classes="ssv-svg--inline ssv-svg--ic-bubble"/>
                <span>Bubble Sort</span>
            </li>
        </ul>
    </div>

    <button class="ssv-btn ssv-btn--primary ssv-btn--generate" on:click={() => dispatch('generate')}>
        Generate New Dataset
    </button>
</aside>

<style type="text/scss">
    @import "../styles/settings.scss";

    .ssv-sidebar {
        @include ssv-size(15%, calc(100vh - 70px));

        background-color: $c-secondary;
        padding: 50px 30px;

        .ssv-sorts {
            border-bottom: 2px solid rgba($c-basic, 0.2);
            padding-bottom: 50px;
            margin: 10px 0 60px;

            .ssv-h4 {
                color: rgba($c-basic, 0.2);
                margin: 0 0 10px;
            }

            .ssv-menu {
                margin: 0 -30px;

                .ssv-menu__item {
                    @include ssv-size(100%, auto);

                    position: relative;
                    display: flex;
                    justify-content: flex-start;
                    align-items: center;
                    overflow: hidden;
                    padding: 15px 30px;
                    cursor: pointer;
                    transition: background-color 0.3s ease-in-out;

                    span {
                        z-index: 1;
                        font-size: 1.5rem;
                        font-weight: 400;
                        letter-spacing: 0.5px;
                        line-height: 1;
                        color: rgba($c-basic, 0.4);
                    }

                    &::after {
                        @include ssv-pseudo(inline-flex, relative);
                        @include ssv-size(6px);

                        background-color: transparent;
                        margin: 0 0 0 auto;
                        transition: background-color 0.3s ease-in-out;
                    }

                    &.ssv-active,
                    &:hover {
                        background-color: $c-dark;
                    }

                    &.ssv-active::after {
                        background-color: $c-primary;
                    }
                }
            }
        }

        .ssv-btn--generate {
            margin: 0 auto;
        }
    }
</style>