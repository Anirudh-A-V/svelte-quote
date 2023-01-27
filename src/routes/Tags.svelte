<script lang="ts">

    import { onMount } from 'svelte';
    
    import { selectedTag } from './store.js';

    let tags: any = [];

    const getTags = async () => {
        const response = await fetch('https://api.quotable.io/tags');
        const data = await response.json();

        tags = data.map((tag: any) => tag.name);
    };

    onMount(() => {
        getTags();
    });

    const setTag = (e: any) => {
        selectedTag.set(e.target.value)
    };

</script>   

<div class="tags-body">
    <div class="tags">
        <!-- Dropdown -->
        <select class="dropdown">
            <option value="all" selected on:click={setTag}>All</option>
            {#each tags as tag}
                <option value={tag} on:click={setTag}>{tag}</option>
            {/each}
        </select>
    </div>
</div>

<style>
    .tags-body {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100%;
        padding: 1rem;
        background-color: #f5f5f5;
        border-radius: 15px;
    }

    .tags {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100%;
        padding: 1rem;
    }

    .dropdown {
        width: 100%;
        padding: 0.5rem;
        border: 1px solid #ccc;
        border-radius: 5px;
        outline: none;
    }

    .dropdown:focus {
        border: 1px solid #000;
    }

    .dropdown option {
        padding: 0.5rem;
    }

    .dropdown option:hover {
        background-color: #ccc;
    }

    .dropdown option:active {
        background-color: #000;
        color: #fff;
    }


</style>