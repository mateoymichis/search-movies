<script>
    import {API_KEY} from '../key.js';
    import Movie from './Movie.svelte';
    let value = '';
    let response = [];
    const handleInput = (event) => value = event.target.value;

    $: if (value.length > 2){
       response = fetch(`https://www.omdbapi.com/?s=${value}&apikey=${API_KEY}`)
       .then(res => res.json())
       .then(apiResponse => apiResponse.Search || [])
    }
</script>

<input placeholder="Search movies" value={value} on:input={handleInput} type="text">

{#await response}
    <strong>Loading...</strong>
{:then movies}
    {#each movies as {Title, Poster, Year}, index}
    <Movie 
        index={index}
        title={Title}
        poster={Poster}
        year={Year}
    />
    {:else}
    <strong>No hay resultados</strong>
    {/each}  
{/await}

