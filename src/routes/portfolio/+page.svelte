<script>
// @ts-nocheck
    import { onMount } from 'svelte'
    import { selectedAccount ,defaultEvmStores} from 'svelte-web3'

    onMount(async () => {
        await defaultEvmStores.setProvider()})
        
    async function getNftList() {
        const res = await fetch(`https://express-api.codeboxxtest.xyz/NFT/getWalletTokens/0x5f927157539C9f690F1f381c8Ba6Add22d84325C`)
        console.log();
        // const res = await fetch(`https://express-api.codeboxxtest.xyz/NFT/getWalletTokens/${selectedAccount}`)
        const nfts = await res.json()

        if (res.ok) {
			return nfts;
		} else {
			return  [];
		}
    }  

    let nft_list = getNftList()

    nft_list.then(res => console.log(res))
    console.log($selectedAccount)
</script>

<div class="index">
    <h2>NFTs</h2>
    <p>USER ADDRESS : {$selectedAccount}</p>
    {#await nft_list}
	<p>...LOADING</p>
    {:then nft_list}
    <div class="list">
        {#each nft_list as {name, description, image}}
            <div class="item">
                <h3>{name}</h3>
                <p>{description}</p>
                <img height="300" src={ image }	alt={ name }/>
            </div>
        {/each}
    </div>
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
</style>