<script context="module">
  let allVideos = [];

  export function getAllVideosLength() {
    allVideos.forEach((vid) => console.log(vid));
  }
</script>

<script>
  import { onDestroy, onMount } from 'svelte';

  export let src = undefined;

  let paused = true;

  let video;
  let newEntry;
  const id = new Date().getTime() + Math.floor(Math.random() * 100 + 1).toString();

  onMount(() => {
    newEntry = { id, video };
    allVideos.push(newEntry);
  });
  onDestroy(() => {
    allVideos = allVideos.filter((vid) => vid.id !== newEntry.id);
  });
</script>

<video
  bind:this={video}
  class:playing={!paused}
  {src}
  controls
  muted
  bind:paused
  on:play={() =>
    allVideos.forEach((entry) => {
      if (entry.id !== newEntry.id) {
        entry.video.pause();
        entry.video.currentTime = 0;
      }
    })}
/>

<button on:click={() => (paused = !paused)}>{paused ? 'Play' : 'Pause'}</button>
