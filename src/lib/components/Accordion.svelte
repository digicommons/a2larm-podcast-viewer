<script>
	let isOpen = false;
	const toggle = () => isOpen = !isOpen
</script>

<section>
  <button
    on:click={toggle}
    aria-expanded={isOpen}
  >
    <svg
      style="tran"
      width="10"
      height="10"
      fill="none"
      stroke-linecap="round"
      stroke-linejoin="round"
      stroke-width="2"
      viewBox="0 0 24 24"
      stroke="currentColor"
    >
      <path d="M9 5l7 7-7 7"></path>
    </svg>
    O těchto stránkách
  </button>
  
  {#if isOpen}
  <p>Alarm produkuje více než tucet skvělých podcastů. Pokud jste ale trochu jako já, určitě jste si už zanadávali, proč musím odebírat hned všechny najednou, když jinde jde odebírat podcast po podcastu.</p>
  <p>Jednak, protože jsem tento problém chtěl pro sebe vyřešit, jednak, protože mě baví vyrábět aplikace, vám na těchto stránkách nabízím (neúplný, ale snad aktuální) přehled alarmáckých podcastů a možnost je jednotlivě odebírat ve vaší oblíbené podcastové aplikaci.</p>
  <p>Máte-li nápad na vylepšení nebo pokud vás zajímá, jak aplikace funguje, určitě se podívejte na <a href="https://github.com/digicommons/a2larm-podcast-parser" target="_blank">GitHub</a>!</p>
  {/if}
</section>


<style>
  section {
    margin: 0 auto 1rem auto;
    max-width: 95%;
  }

  @media (min-width: 480px) {
    section {
      max-width: 35rem;
    }
  }

	button {
    border: none;
    background: none;
    display: block;
    color: inherit;
    cursor: pointer;
    font-size: .9rem;
    margin: 0;
    padding-bottom: 0.5em;
    padding-top: 0.5em
  }

  p {
    font-size: .9rem;
  }

	svg {
    transition: transform 0.2s ease-in;
	}
	
	[aria-expanded=true] svg {
    transform: rotate(0.25turn);
  }
</style>