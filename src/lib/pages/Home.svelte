<script>
  import VideoPlayerReRedo, { logAllVideoInstances } from '../VideoPlayerReRedo.svelte';
  import { default as videoLoc } from '../../../public/mov_bbb.mp4';

  let show = true;
</script>

<button on:click={() => logAllVideoInstances()}>LOG LENGTH</button>
<button on:click={() => (show = !show)}>HIDE LAST</button>

<!-- <VideoPlayerReRedo src={videoLoc} />
<VideoPlayerReRedo src={videoLoc} />
{#if show}
  <VideoPlayerReRedo src={videoLoc} />
{/if} -->

<style lang="css"></style>
