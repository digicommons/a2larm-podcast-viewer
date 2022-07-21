<script>
  import FeedFetcher from './lib/components/FeedFetcher.svelte';
  import Accordion from './lib/components/Accordion.svelte';
</script>

<main>
  <h1>A2larm podcasts</h1>
  <Accordion />
  <FeedFetcher />
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    padding: 1em;
    margin: 0 auto;
  }

  h1 {
    text-align: center;
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto 1rem auto;
  }
</style>
