<script>
    let pokemonName = ''

    function logIt() {
        console.log(pokemonName)
    }
</script>

<input type="text" bind:value={pokemonName} placeholder="Enter Pokemon name" />
<button on:click={logIt}>Search</button>
