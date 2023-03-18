<script>
    export let index, title, poster, year;
</script>

<style>
    article {
        border: 1px solid #eee;
        border-radius: 4px;
        padding: 16px;
        margin-bottom: 8px;

    }

    h3 {
        font-size: 24px;
        margin-bottom: 4px;

    }
</style>

<article>
    <p>#{index}</p>
    <img src={poster} alt={title}>
    <h3>{title}</h3>
    <span>{year}</span>
{#if 2022-year < 5}
    <i>🆕</i>
{/if}
</article>  
