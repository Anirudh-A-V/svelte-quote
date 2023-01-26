<script>
    import { onMount } from 'svelte';
	import Tags from './Tags.svelte';

    let quote = '';
    let author = '';

    const getQuote = async () => {
        const response = await fetch('https://api.quotable.io/random');
        const data = await response.json();

        quote = data.content
        console.log(data);
        author = data.author;
    };

    onMount(() => {
        getQuote();
    });
</script>

<div class="quote-body">
    <div class="body">
        <p class="quote">"{quote}"</p>
        <p class="author">- {author}</p>

        <button class="btn" on:click={getQuote}>
            <!-- Text SVG -->
            <span>Get Quote</span>
        </button>
    </div>
    <Tags />
</div>

<style>
    .quote-body {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100%;
        padding: 1rem;
        background-color: #f5f5f5;
        border-radius: 15px;
    }

    .body {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100%;
        padding: 1rem;
    }
    .quote {
        font-size: 1.5rem;
        font-weight: 500;
        margin-bottom: 1rem;
    }

    .author {
        font-size: 1.2rem;
        font-weight: 400;
        margin-bottom: 1rem;
    }

    .btn {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 0.5rem 1rem;
        border: 1px solid var(--color-bg-1);
        border-radius: 0.25rem;
        background-color: var(--color-bg-1);
        color: var(--color-text-1);
        font-size: 1rem;
        font-weight: 500;
        cursor: pointer;
        transition: all 0.2s ease-in-out;
    }

    .btn:hover {
        background-color: var(--color-bg-2);
    }

    /* .btn svg {
        width: 1.5rem;
        height: 1.5rem;
        margin-right: 0.5rem;
    } */
</style>