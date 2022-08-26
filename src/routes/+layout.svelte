<script>
import Footer from "../lib/footer.svelte";
import Header from "../lib/header.svelte";

</script>

<header>
    <Header/>
</header>

<main>
    <slot></slot>
</main>

<footer>
    <Footer/>
</footer>

<style>
</style>