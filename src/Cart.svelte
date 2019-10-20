<script>
    export let items;

    //$: is actually a regular Javascript syntax. It's called a labeled statement
    // You typically don't use it. You could use it in conjunction with loops and to continue and break keywords
    // Svelte hijacks it and make sure that whatever you write after this label will be re-executed by svelte
    // whenever one of its input values changes
    //
    // My questions: Why didn't it need let in front of carTotal?
    $: cartTotal = items.reduce((sum, curValue) => {
        return sum + curValue.price;
    }, 0);
</script>

<style>
    ul {
        list-style: none;
        margin: 1rem;
        padding: 0;
    }

    li {
        margin: 0.5rem 0;
        padding: 0.5rem;
        border: 1px solid #ccc;
    }

    h1 {
        font-size: 1.5rem;
        margin: 1rem;
    }
</style>

{#if items.length === 0}
    <p>No items in cart yet.</p>
{:else}
    <ul>
        {#each items as item}
            <li>{item.title} - {item.price}</li>
        {/each}
    </ul>

    <h1>TOTAL: ${cartTotal}</h1>
{/if}
