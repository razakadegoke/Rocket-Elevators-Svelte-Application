<script>
   // @ts-nocheck
    import { onMount } from 'svelte';
    import { goto } from '$app/navigation';
    import { defaultEvmStores, selectedAccount } from 'svelte-web3'

    onMount(async () => {
        await defaultEvmStores.setProvider()
        const eligible = await (await fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/${$selectedAccount}`)).json()
        console.log(eligible)
        if (eligible) {
            await fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/${$selectedAccount}`,{
            method : 'POST'
        })}
    }) 
    const connect_metamask = () => defaultEvmStores.setProvider()
    const goto_portfolio = () => goto("/portfolio")
</script>

<div>
    <p>Home Page</p>
    {#if $selectedAccount != null}
        <p>Your are connected!</p>
        <p>Your address : {$selectedAccount}</p>
        <button on:click={goto_portfolio}>GO TO YOUR PORTFOLIO</button>
    {:else}
        <p>Your are not connected!</p>
        <button on:click={connect_metamask}>CONNECT YOUR ACCOUNT</button>
    {/if}
</div>

<style>

</style>