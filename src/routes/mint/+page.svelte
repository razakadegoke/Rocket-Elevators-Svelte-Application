<script>
    import { onMount } from "svelte"
    import { selectedAccount, defaultEvmStores} from "svelte-web3"
    
    let balance = 0

    const getUserBalance = async () => {
        const res = await fetch(`https://express-api.codeboxxtest.xyz/ERC20/balance/${$selectedAccount}`)
        const rep = await res.json()

        if (res.ok) {
            console.log(`SUCCEED: ${res.status}`)
            console.log(`USER BALACE : ${rep}`)
            return rep
        }else{
            console.log(`ERROR: ${res.status}`)
            return 0
        }
    }
    const generateNft = async () => {
        const res = await fetch(`https://express-api.codeboxxtest.xyz/NFT/buyWithRocket/${$selectedAccount}`,{
            method: "POST"
        })
        const rep = await res.text()

        if (res.ok) {
            console.log(`SUCCEED: ${res.status}`)
            return rep
        }else{
            console.log(`ERROR: ${res.status}`)
        }
    }   

    onMount(async () => {
        await defaultEvmStores.setProvider()
        balance = await getUserBalance() 
    })

</script>

<div class="mint">
    <h2>GENERATE NEW NFT</h2>
    <p>Your address : {$selectedAccount}</p>
    <p>Your ROCKET TOKEN balance : {balance}</p>
    {#if balance < 100}
        <p>Sorry you don't have enough ROCKET TOKEN</p>
        <button><a href="/">GO HOME</a></button>
    {:else}
        <button on:click={generateNft}>GET ONE</button>
    {/if}
    <iframe src="https://giphy.com/embed/wRCu1p7zjO2BQWgFNk" width="480" height="200" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>
</div>

<style>
    .mint{
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 50px;
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