<script>
    import {API_KEY} from '../key.js';
    import Movie from './Movie.svelte';
    let value = '';
    let loading = false;
    let response = [];
    const handleInput = (event) => value = event.target.value;

    $: if (value.length > 2){
        loading = true;
       fetch(`https://www.omdbapi.com/?s=${value}&apikey=${API_KEY}`)
       .then(res => res.json())
       .then(apiResponse => {
            response = apiResponse.Search || [];
            loading = false;
       })
    }
</script>

<input placeholder="Search movies" value={value} on:input={handleInput} type="text">

{#if loading}
    <strong>Loading...</strong>
{:else}
    {#each response as {Title, Poster, Year}, index}
    <Movie 
        index={index}
        title={Title}
        poster={Poster}
        year={Year}
    />
    {:else}
    <strong>No hay resultados</strong>
    {/each}
{/if}

