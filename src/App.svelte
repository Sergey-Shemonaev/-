<script>
  import svelteLogo from './assets/svelte.svg'
  import Cards from './lib/Cards.svelte'
  import Bocks from "./lib/Bocks.svelte";
  import Visiors from './lib/Visiors.svelte';
  
  $: visible =true


  $: cklicys =()=>{
    console.log('lol Lol LOL');
    visible = !visible
  }
  let box = Bocks
</script>


<div class="contenier">
  <section>
    <h2><p>LIBRARY</p></h2>
  </section>
  <nav>
    <button  id="Books"  on:click={() => {box = Bocks}} >Bocks</button>
    <button  id="visitors" on:click={() => {box = Visiors }} >Visitior</button>
    <button id="cards" on:click={() => {box = Cards}} >Cards</button>
    <button  id=""   >Statistics</button>
  </nav>
</div>

<svelte:component this="{box}" />

<style>

</style>
