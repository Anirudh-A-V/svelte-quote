<script lang="ts">

    import { onMount } from 'svelte';

    let tags: any = [];

    const getTags = async () => {
        const response = await fetch('https://api.quotable.io/tags');
        const data = await response.json();

        tags = data.map((tag: any) => tag.name);
    };

    onMount(() => {
        getTags();
    });
</script>

<div class="tags-body">
    <div class="tags">
        {#each tags as tag}
            <a href="/" class="tag">{tag}</a>
        {/each}
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

    .tag {
        font-size: 1.5rem;
        font-weight: 500;
        margin-bottom: 1rem;
    }

</style>