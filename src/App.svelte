<script>
    import Product from "./Product.svelte";
    import Button from './Button.svelte';

    let title = '';
    let price = 0;
    let description = '';

    let products = [];

    function setTitle(event) {
        title = event.target.value;
    }
    
    function createProduct() {
        const newProduct = {
            title,
            price,
            description
        };
        products.push(newProduct);
    }
</script>

<style>
    section {
        width: 30rem;
        margin: auto;
    }

    label, input, textarea {
        width: 100%;
    }
</style>

<!-- Can do on:click, on:blur, on:input        -->

<p>{title}</p>
<section>
    <div>
        <label for="title">Title</label>
        <input type="text" id="title" value="{title}" on:input="{setTitle}"/>
    </div>
    <div>
        <label for="price">Price</label>
        <input type="number" id="price" bind:value={price}/> <!-- svelte will convert the price into a number for us -->
    </div>
    <div>
        <label for="description">Description</label>
        <textarea rows="3" id="description" bind:value={description}></textarea>
    </div>

    <Button on:click={createProduct}>Create Product</Button>
</section>

<Product productTitle={title} productPrice={price} productDescription={description} />
