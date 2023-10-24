<script context="module">
  // we're creating an array that will hold all the instances, so we can pause the other videos if we have one playing
  let allVideos = new Set();
</script>

<script>
  import { onDestroy, onMount } from 'svelte';

  export let src = undefined;

  let paused = true;
  // the reference to bind the node to
  let video;

  onMount(() => allVideos.add(video));
  onDestroy(() => allVideos.delete(video));
  //   let currentTime = 0;
  //   let volume = 0;
</script>

<button on:click={() => console.log(allVideos.size)}>BTN</button>
<video
  bind:this={video}
  class:playing={!paused}
  {src}
  controls
  muted
  bind:paused
  on:play={() =>
    allVideos.forEach((vid) => {
      // if the CB is not equal to this instance
      if (vid !== video) {
        vid.pause();
      }
    })}
/>

<button on:click={() => (paused = !paused)}>{paused ? 'Play' : 'Pause'}</button>

<!-- <p>{currentTime}</p>
<p>{volume}</p> -->

<style lang="css">
  .playing {
    outline: 4px solid #ff3e00;
  }
</style>
