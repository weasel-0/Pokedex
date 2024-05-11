<script>
    let pokemonName = ''
    let pokemon = null
    let error = null
    let colors = {
        normal: '#D0B794',
        fire: '#FED29E',
        water: '#98DBFE',
        electric: '#FFEB93',
        grass: '#A3CF92',
        ice: '#CAEDED',
        fighting: '#E39590',
        poison: '#D19DD2',
        ground: '#F3E1B0',
        flying: '#D2C5FA',
        psychic: '#FFA7C2',
        bug: '#D6E08C',
        rock: '#DFD199',
        ghost: '#B7AACD',
        dragon: '#B697FF',
        dark: '#B9ABA3',
        steel: '#DBDBE8',
        fairy: '#F9D9DC',
    }

    async function fetchPokemon() {
        try {
            let url = 'https://pokeapi.co/api/v2/pokemon/'
            let response = await fetch(`${url}${pokemonName}`)
            if (!response.ok) {
                throw new Error('Pokemon not found')
            }
            let { name, sprites, stats, types } = await response.json()
            pokemon = {
                name,
                // image: sprites.versions['generation-ii']['gold']
                //     .front_transparent,
                image: sprites.front_default,
                hp: stats[0].base_stat,
                attack: stats[1].base_stat,
                defense: stats[2].base_stat,
                color: types[0].type,
            }
            error = null
        } catch (err) {
            pokemon = null
            error = err.message
        }
    }

    async function doStuff() {
        try {
            await fetchPokemon()
            // console.log(pokemon.color)
            document.documentElement.style.setProperty(
                '--pixel-bg',
                colors[pokemon.color.name]
            )
        } catch (err) {
            console.error(err)
        }
    }

    function handleKeyDown(event) {
        if (event.key === 'Enter') {
            document.querySelector('button').click()
        }
    }
</script>

<!-- svelte-ignore a11y-autofocus -->
<div class="nav">
    <img src="src/assets/Pokedex_logo.png" alt="pokedex" class="logo" />
    <div class="searchBar">
        <input
            spellcheck="false"
            type="text"
            bind:value={pokemonName}
            placeholder="Enter Pokemon name"
            autofocus
            on:keydown={handleKeyDown}
        />
        <button on:click={doStuff}>search</button>
    </div>
</div>
<section class="container">
    {#if pokemon}
        <div class="pixel-border">
            <h1>{pokemon.name}</h1>
            <img src={pokemon.image} alt={pokemon.name} class="pokemonImage" />
            <h2>HP : {pokemon.hp}</h2>
            <h2>Type : {pokemon.color.name}</h2>
            <h2>Attack : {pokemon.attack}</h2>
            <h2>Defence : {pokemon.defense}</h2>
        </div>
    {:else if error}
        <p>{error}</p>
    {/if}
</section>

<style>
    @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

    button {
        width: 64px;
        height: auto;
        border-radius: 0 10px 10px 0;
        border: double #000;
        border-left: none;
        background-color: #f5eddc;
        font-family: 'VT323';
        font-size: 18px;
        box-shadow: 5px 5px 10px 0px rgba(0, 0, 0, 0.2);
    }
    .nav {
        display: grid;
        gap: 20px;
        align-items: center;
        place-items: center;
        padding: 10px;
    }

    .logo {
        max-height: 150px;
        max-width: 150px;
    }

    .searchBar {
        display: flex;
        justify-content: center;
    }

    :root {
        background-image: url('src/assets/retro-2.jpg');
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
        height: 32px;
        padding: 4px;
        border: 1px solid black;
        font-size: 24px;
        font-family: 'VT323';
        border-radius: 10px 0 0 10px;
        border: 0;
        border: double #000;
        border-right: none;
        background-color: #f5eddc;
        box-shadow: 5px 5px 10px 0px rgba(0, 0, 0, 0.2);
    }

    input:focus {
        outline: 0;
    }

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
        --pixel-bg: #fff; /* Inner background color #f5eddc*/
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

    section {
        margin: auto;
        width: 290px;
        height: 336px;
        padding-inline: min(5vw, 1em);
        text-align: center;
    }
    h1 {
        font-size: clamp(0.625rem, calc(0.625rem + 4vw), 2rem);
    }
</style>
