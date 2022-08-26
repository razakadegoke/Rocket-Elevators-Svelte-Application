<script>
// @ts-nocheck
    import { onMount } from 'svelte'
    import { selectedAccount ,defaultEvmStores} from 'svelte-web3'

    onMount(async () => {
        await defaultEvmStores.setProvider()})
        
    async function getNftList() {
        // const res = await fetch(`https://express-api.codeboxxtest.xyz/NFT/getWalletTokens/${$selectedAccount}`)
        const res = await fetch(`https://express-api.codeboxxtest.xyz/NFT/getWalletTokens/0x1E90cf48F11Dd52802eC7D1AF7082122A6a59312`)
        const nfts = await res.json()

        if (res.ok) {
			return nfts;
		} else {
			return  [];
		}
    }  

    let nft_list = getNftList()
</script>

<div class="index">
    <h2>NFTs</h2>
    <p>USER ADDRESS : {$selectedAccount}</p>
    {#await nft_list}
	<iframe src="https://giphy.com/embed/pK4av7uBK3I4M" width="480" height="221" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>
    {:then nft_list}
        {#if nft_list.length === 0}
            <p>No NFTs...</p>
            <button><a href="/mint">BUY NOW</a></button>
            <iframe src="https://giphy.com/embed/3o6Zt4oEFxYJQBIk48" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>
        {:else}
            <div class="list">
                {#each nft_list as {name, description, image}}
                    <div class="item">
                        <h3>{name}</h3>
                        <p>{description}</p>
                        <img height="300" src={ image }	alt={ name }/>
                    </div>
                {/each}
            </div>
        {/if}
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}
</div>

<style> 
    .index{
        text-align: center;
    }

    .list {
        display: flex;
        flex-wrap: wrap;
        flex-direction: row;
        gap:50px;
        justify-content : center;
        
    }

    .item{
        background-color: #211724;
        border: 16px solid transparent;
        border-image: linear-gradient(45deg, #b51021 , #0873bb);
        border-image-slice: 1;
        padding: 30px;
    }

    button {
        background-image: linear-gradient(to right, #b51021 0%, #0873bb  51%, #b51021  100%);
        border: 0px;
        margin: auto;
        margin-bottom: 20px;
        padding: 15px 45px;
        text-align: center;
        display: block;
        text-transform: uppercase;
        transition: 0.5s;
        background-size: 200% auto;
        color: white;            
    }

    button:hover {
        background-position: right center;
        color: #fff;
        text-decoration: none;
    } 
</style>