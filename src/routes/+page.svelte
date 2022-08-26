<script>
   // @ts-nocheck
    import { onMount } from 'svelte';
    import { goto } from '$app/navigation';
    import { defaultEvmStores, selectedAccount } from 'svelte-web3'

    onMount(async () => {
        await defaultEvmStores.setProvider()
        const eligible = await (await fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/${$selectedAccount}`)).json()
        if (eligible) {
            await fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/${$selectedAccount}`,{
            method : 'POST'
        })}
    }) 
    const connect_metamask = () => defaultEvmStores.setProvider()
    const goto_portfolio = () => goto("/portfolio")
</script>

<div class="home">
    <div class="banner">
        <h1 style=" background : linear-gradient(45deg, #b51021 , #0873bb);">DISCOVER, COLLECT, AND CHARITY IN EXTRAORDINARY NFT MARKETPLACE</h1>
        <iframe src="https://giphy.com/embed/3o6ZtikKNHU8eMFaww" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>
        <p>n aenean posuere lorem risus nec. Tempor tincidunt aenean purus purus vestibulum nibh mi venenatis</p>
        {#if $selectedAccount != null}
            <p>Your are connected!</p>
            <p>Your address : {$selectedAccount}</p>
            <button on:click={goto_portfolio}>GO TO YOUR PORTFOLIO</button>
        {:else}
            <p>Your are not connected!</p>
            <button on:click={connect_metamask}>CONNECT YOUR ACCOUNT</button>
        {/if}
    </div>
</div>

<style>  
    h1{
        background-color: linear-gradient(to right, #b51021 0%, #0873bb  51%, #b51021  100%);
    }
    .home{
        display: flex;
        justify-content: space-around;
    }

    .home p{
        text-align: left;
        font-size: 1.25rem;
        line-height: 1.75rem;
        max-width: 28rem;
    }

    .banner{
        max-width: 42rem;
    }

    .banner h1{
        font-size: 3.75rem;
        line-height: 1;
        text-align: left;
    }

    button {
        background-image: linear-gradient(to right, #b51021 0%, #0873bb  51%, #b51021  100%);
        border: 0px;
        margin: 10px;
        padding: 15px 45px;
        text-align: center;
        text-transform: uppercase;
        transition: 0.5s;
        background-size: 200% auto;
        color: white;            
        display: block;
    }

    button:hover {
        background-position: right center;
        color: #fff;
        text-decoration: none;
    } 
</style>