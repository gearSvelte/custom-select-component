<script lang="ts">
  let breed = 'whippet';
  async function getDogsImage(): Promise<string[]> {
    const url = `https://dog.ceo/api/breed/${breed.toLowerCase()}/images/random/1`;
    const response = await fetch(url);
    if (!response.ok || response.status === 404) return [];
    const json = await response.json();
    return json.message;
  }
  let dogs = getDogsImage();
</script>

<section>
  <label for="breed">breed</label>
  <input type="text" id="breed" bind:value={breed} />
  <button on:click={() => (dogs = getDogsImage())} type="button"
    >get dog image</button
  >
  <h1>image of {breed} dog</h1>
  {#await dogs}
    <h3>waiting for dog's image ...</h3>
  {:then imageUrls}
    {#each imageUrls as url}
      <figure>
        <img src={url} alt="dog" />
      </figure>
    {:else}
      <h3>nothing found</h3>
    {/each}
  {:catch error}
    <h3>Error: {error.message}</h3>
  {/await}
</section>

<style></style>
