<script>
  import MusicCard from '../components/MusicCard.svelte';

  import { MUSIC_CARDS } from '../mock-data.js';

  let musicCards = MUSIC_CARDS;
</script>

<style>
</style>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>

<div class="dashboard">
  <div class="music-cards">
    {#each musicCards as musicCard}
      <MusicCard 
        {musicCard}>
      </MusicCard>
    {:else}
      <p>SONGS NOT EVEN ONCE</p>
    {/each}
  </div>
</div>
<a rel=prefetch href="player">player</a>