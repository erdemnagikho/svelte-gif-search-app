<script>
  let search = "";
  let loading = false;
  const API_URL =
    "https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=";
  let gifs = [];

  async function formSubmitted(event) {
    event.preventDefault();
    loading = true;
    gifs = [];
    const url = `${API_URL}${search}`;
    const response = await fetch(url);
    const json = await response.json();
    gifs = json.data.map(gif => gif.images.fixed_height.url);
    loading = false;
  }
</script>

<style>
  .results {
    column-count: 3;
  }
  img {
    width: 100%;
    height: auto;
  }
</style>

<form on:submit={formSubmitted}>
  <label for="search">Search</label>
  <input bind:value={search} id="searh" name="search" type="text" />
  <button type="submit">GO!</button>
</form>

<div class="results">
  {#each gifs as gif}
    <img alt="gif" src={gif} />
  {/each}
</div>
