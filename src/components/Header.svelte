<script>
    import {createEventDispatcher} from 'svelte';
    import AssetSVG from './AssetSVG.svelte';
    import logo from '../../public/img/icons/logo.svg';

    const dispatch = createEventDispatcher();
</script>

<header class="ssv-header">
    <div class="ssv-logo">
        <AssetSVG src={logo} classes="ssv-svg--logo"/>
        <h1 class="ssv-title">SSV</h1>
    </div>

    <button class="ssv-btn ssv-btn--primary ssv-btn--start-stop" on:click={()=> dispatch('start')}>Start</button>
</header>

<style type="text/scss">
    @import "../styles/settings.scss";

    .ssv-header {
        position: relative;
        display: flex;
        justify-content: space-between;
        align-items: stretch;
        background-color: $c-secondary;

        .ssv-logo {
            @include ssv-size(15%, auto);

            display: flex;
            justify-content: flex-start;
            align-items: center;
            background-color: $c-primary;
            padding: 10px 20px;

            .ssv-title {
                font-size: 40px;
                color: $c-basic;
            }
        }

        .ssv-btn--start-stop {
            font-size: 22px;
            font-weight: 700;
            letter-spacing: 1.5px;
            border-radius: 0;
            background-color: $c-tertiary;
            padding: 15px 50px;

            &:hover {
                background-color: $c-tertiary--hover;
            }
        }
    }
</style>