<script>
    /*
1. input and search(input needs to be name)
2. random button to generate 10 random pokemon(random is based on id)
*/
    let pokemonName = ''
    let pokemon = null
    let error = null

    async function fetchPokemon() {
        try {
            let url = 'https://pokeapi.co/api/v2/pokemon/'
            let response = await fetch(`${url}${pokemonName}`)
            if (!response.ok) {
                throw new Error('Pokemon not found')
            }
            let { name, sprites } = await response.json()
            pokemon = {
                name,
                image: sprites.versions['generation-ii']['gold']
                    .front_transparent,
            }
            error = null
        } catch (err) {
            pokemon = null
            error = err.message
        }
    }
</script>

<div class="nav">
    <img src="src/assets/Pokedex_logo.png" alt="pokedex" class="logo" />
    <div class="searchBar">
        <input
            type="text"
            bind:value={pokemonName}
            placeholder="Enter Pokemon name"
        />
        <button on:click={fetchPokemon}>Search</button>
    </div>
</div>
<section class="container">
    {#if pokemon}
        <div class="pixel-border">
            <h1>{pokemon.name}</h1>
            <img src={pokemon.image} alt={pokemon.name} class="pokemonImage" />
        </div>
    {:else if error}
        <p>{error}</p>
    {/if}
</section>

<!-- <script>
    const maxPokemon = 151
    let pokemonName
    async function fetchPokemon(id){
      let url = 'https://pokeapi.co/api/v2/pokemon/'
      let response = await fetch (`${url}${id}`)
      let {name, sprites} = await response.json()
    }
</script> -->

<style>
    @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

    .nav {
        display: grid;
        grid-template-columns: auto 1fr; /* First column for logo, second column for search bar */
        align-items: center; /* Center items vertically */
        padding: 10px; /* Add padding for spacing */
    }

    .logo {
        max-height: 150px; /* Adjust the height of the logo as needed */
        max-width: 150px; /* Adjust the width of the logo as needed */
    }

    .searchBar {
        display: flex;
        justify-content: center; /* Center items horizontally */
    }

    .searchBar input {
        margin-right: 10px; /* Add margin between input and button */
    }

    :root {
        background-color: #f5eddc;
        height: 100vh;
        font-family: 'VT323', monospace;
        font-weight: 400;
        font-style: normal;
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    input {
        width: 350px;
        height: 28px;
        padding: 2px;
        border: 1px solid black;
        font-size: 18px;
    }
    /* .card {
        width: 240px;
        height: 336px;
        background-color: darkgray;
        border: 1px solid black;
    } */
    img {
        image-rendering: pixelated;
    }

    .pokemonImage {
        width: 200px;
        height: auto;
    }

    .logo {
        width: 200px;
        height: auto;
    }

    :root {
        --pixel-bg: #f5eddc; /* Inner background color */
        --pixel-border: black; /* Inner border color: */
        --pixel-border-2: white; /* Middle border color: */
        --pixel-border-3: var(--pixel-border); /* Outer border color */
        --pixel: 0.125rem; /* Pixel size */
    }

    .pixel-border {
        background: var(--pixel-bg);
        box-shadow:

	/* Inner Background Color */
            0 calc(var(--pixel) * -3) 0 calc(var(--pixel) * -1) var(--pixel-bg),
            0 calc(var(--pixel) * 3) 0 calc(var(--pixel) * -1) var(--pixel-bg),
            0 calc(var(--pixel) * -6) 0 calc(var(--pixel) * -2) var(--pixel-bg),
            0 calc(var(--pixel) * 6) 0 calc(var(--pixel) * -2) var(--pixel-bg),
            0 calc(var(--pixel) * -9) 0 calc(var(--pixel) * -4) var(--pixel-bg),
            0 calc(var(--pixel) * 9) 0 calc(var(--pixel) * -4) var(--pixel-bg),
            0 calc(var(--pixel) * -12) 0 calc(var(--pixel) * -6) var(--pixel-bg),
            0 calc(var(--pixel) * 12) 0 calc(var(--pixel) * -6) var(--pixel-bg),
            /* Pixel Border Layer 1 */ calc(var(--pixel) * -1) 0 0 0
                var(--pixel-border),
            var(--pixel) 0 0 0 var(--pixel-border),
            0 calc(var(--pixel) * -2) 0 0 var(--pixel-border),
            0 calc(var(--pixel) * 2) 0 0 var(--pixel-border),
            0 calc(var(--pixel) * -5) 0 calc(var(--pixel) * -1)
                var(--pixel-border),
            0 calc(var(--pixel) * 5) 0 calc(var(--pixel) * -1)
                var(--pixel-border),
            0 calc(var(--pixel) * -7) 0 calc(var(--pixel) * -2)
                var(--pixel-border),
            0 calc(var(--pixel) * 7) 0 calc(var(--pixel) * -2)
                var(--pixel-border),
            0 calc(var(--pixel) * -10) 0 calc(var(--pixel) * -4)
                var(--pixel-border),
            0 calc(var(--pixel) * 10) 0 calc(var(--pixel) * -4)
                var(--pixel-border),
            0 calc(var(--pixel) * -13) 0 calc(var(--pixel) * -6)
                var(--pixel-border),
            0 calc(var(--pixel) * 13) 0 calc(var(--pixel) * -6)
                var(--pixel-border),
            /* Pixel Border Layer 2 */ calc(var(--pixel) * -2) 0 0 0
                var(--pixel-border-2),
            calc(var(--pixel) * 2) 0 0 0 var(--pixel-border-2),
            0 calc(var(--pixel) * -1) 0 var(--pixel) var(--pixel-border-2),
            0 var(--pixel) 0 var(--pixel) var(--pixel-border-2),
            0 calc(var(--pixel) * -4) 0 0 var(--pixel-border-2),
            0 calc(var(--pixel) * 4) 0 0 var(--pixel-border-2),
            0 calc(var(--pixel) * -6) 0 calc(var(--pixel) * -1)
                var(--pixel-border-2),
            0 calc(var(--pixel) * 6) 0 calc(var(--pixel) * -1)
                var(--pixel-border-2),
            0 calc(var(--pixel) * -8) 0 calc(var(--pixel) * -2)
                var(--pixel-border-2),
            0 calc(var(--pixel) * 8) 0 calc(var(--pixel) * -2)
                var(--pixel-border-2),
            0 calc(var(--pixel) * -11) 0 calc(var(--pixel) * -4)
                var(--pixel-border-2),
            0 calc(var(--pixel) * 11) 0 calc(var(--pixel) * -4)
                var(--pixel-border-2),
            0 calc(var(--pixel) * -14) 0 calc(var(--pixel) * -6)
                var(--pixel-border-2),
            0 calc(var(--pixel) * 14) 0 calc(var(--pixel) * -6)
                var(--pixel-border-2),
            /* Border Layer 3: --pixel-border-3 */ calc(var(--pixel) * -3) 0 0 0
                var(--pixel-border-3),
            calc(var(--pixel) * 3) 0 0 0 var(--pixel-border-3),
            0 0 0 calc(var(--pixel) * 2) var(--pixel-border-3),
            0 calc(var(--pixel) * -3) 0 var(--pixel) var(--pixel-border-3),
            0 calc(var(--pixel) * 3) 0 var(--pixel) var(--pixel-border-3),
            0 calc(var(--pixel) * -5) 0 0 var(--pixel-border-3),
            0 calc(var(--pixel) * 5) 0 0 var(--pixel-border-3),
            0 calc(var(--pixel) * -7) 0 calc(var(--pixel) * -1)
                var(--pixel-border-3),
            0 calc(var(--pixel) * 7) 0 calc(var(--pixel) * -1)
                var(--pixel-border-3),
            0 calc(var(--pixel) * -9) 0 calc(var(--pixel) * -2)
                var(--pixel-border-3),
            0 calc(var(--pixel) * 9) 0 calc(var(--pixel) * -2)
                var(--pixel-border-3),
            0 calc(var(--pixel) * -12) 0 calc(var(--pixel) * -4)
                var(--pixel-border-3),
            0 calc(var(--pixel) * 12) 0 calc(var(--pixel) * -4)
                var(--pixel-border-3),
            0 calc(var(--pixel) * -15) 0 calc(var(--pixel) * -6)
                var(--pixel-border-3),
            0 calc(var(--pixel) * 15) 0 calc(var(--pixel) * -6)
                var(--pixel-border-3);
    }

    /* html,
    body {
	height: 100%;
    }
    body {
	display: grid;
	padding-inline: min(5vw, 1em);
    } */
    section {
        /* margin: auto; */
        width: 240px;
        height: 336px;
        padding-inline: min(5vw, 1em);
        text-align: center;
    }
    h1 {
        font-size: clamp(0.625rem, calc(0.625rem + 4vw), 2rem);
    }
</style>
