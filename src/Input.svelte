<script>
    import {API_KEY} from '../key.js';
    let value = '';

    const handleInput = (event) => value = event.target.value;

    $: if (value.length > 2){
       fetch(`https://www.omdbapi.com/?s=${value}&apikey=${API_KEY}`)
       .then(res => res.json())
       .then(apiResponse => {
            response = apiResponse.Search;
       })
    }
</script>

<input value={value} on:input={handleInput} type="text">