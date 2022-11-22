<script>
  let promise = Promise.resolve([]);

  async function getData(){
    const response = await fetch('https://gist.githubusercontent.com/digicommons/b7fa5297ddb21b46ee63794b5a381098/raw/1a1f2b87618a6bffc58852a07d7f424919a08149/a2larm-feed-2022-11-22.json');
    const data = await response.json();

    return Object.values(data.podcasts);
  }

  let defaultSelect = '';

  promise = getData();

  const getDate = (utc) => {
    const date = new Date(utc);
    const options = { year: 'numeric', month: 'long', day: 'numeric' };

    // @ts-ignore
    return date.toLocaleDateString('cs', options);
  }

  const toLatin = (str) => {
    return str.normalize("NFD")
        .replace(/\p{Diacritic}/gu, "")
        .replace(/\ /g, "_")
        .replace(/[\,\;\:\.\?\!]/g, "")
        .toLowerCase();
  }
</script>

<section>
  <div class="container">
  {#await promise}
    <p>...loading</p>
  {:then podcasts}

    <div class="selectContainer">
      <select bind:value={defaultSelect}>
          <option value="" disabled selected>Vyber si podcast...</option>
        {#each podcasts as podcast}
          <option value={podcast.title}>{podcast.title}</option>
        {/each}
      </select>
    </div>

    <svelte:element this="div">
      {#each podcasts as podcast}
        {#if podcast.title === defaultSelect}
          <h2>{podcast.title}</h2>  
          <div class="podcastDetails">
            <span>Epizod: {Object.keys(podcast).length - 1}</span>
            <a
              href={`https://a2larm-podcast-parser.herokuapp.com/rss/${toLatin(podcast.title)}.rss`}
              class="subscribe"
            >Odebírat</a>
          </div>
          {#each Object.values(podcast).reverse() as episode}
            {#if episode.title !== undefined}
            <div class="episode">
              <h3>{episode.title}</h3>
              <p><span>{getDate(episode.isoDate)}</span><span class="divider">&#8226;</span><a href={episode.link}>Poslechnout</a></p>
              <p class="episodeContent">{episode.content}</p>
            </div>
            {/if}
          {/each}
        {/if}
      {/each}
    </svelte:element>
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
  </div>
</section>

<style>
  section {
    margin: 0 auto;
    max-width: 95%;
  }

  .selectContainer {
    display: flex;
    justify-content: center;
  }

  select {
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    border: 1px solid #ff3e00;
    height: 2rem;
    padding: 0 .5rem;
    background: url(fff-0-2.png) repeat;
    font-family: 'Open Sans', sans-serif;
    font-size: 16px;
  }

  .divider {
    padding: 0 .5rem;
  }

  .podcastDetails {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .subscribe {
    height: max-content;
    padding: .5rem 1rem;
    border-radius: .4rem;
    color: #fff;
    background-color: #ff3e00;
    text-decoration: none;
    font-weight: 600;
  }

  .episode {
    padding: 1rem 0;
    border-bottom: 1px solid #ff3e00;
  }

  .episodeContent {
    white-space: pre-wrap;
  }

  @media (min-width: 480px) {
    section {
      max-width: 35rem;
    }
  }
</style>