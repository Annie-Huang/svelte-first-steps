<script>
    import Product from "./Product.svelte";
    import Button from './Button.svelte';
    import Cart from './Cart.svelte';

    let title = '';
    let price = 0;
    let description = '';

    let products = [];
    let cartItems = [];

    function setTitle(event) {
        title = event.target.value;
    }

    function createProduct() {
        const newProduct = {
            title,
            price,
            description
        };
        // This will not work. push add more value into the array but the array points 'products' still pointing to the same memory location.
        // What we need to do is to assign a new value to product. This will trigger an update by svelte.
        // products.push(newProduct);
        products = products.concat(newProduct);
    }

    function addToCart(event) {
        const selectedTitle = event.detail;
        // It's better if we create a copy of that so that we rule out that we ever mutated this indirectly
        // because such mutations wouldn't be picked up by svelte.
        cartItems = cartItems.concat({
            ...products.find(prod => prod.title === selectedTitle)
        });
        console.log('cartItems=', cartItems);
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

<section>
    <Cart items={cartItems}></Cart>
</section>

<hr/>

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

<section>
    <!--{@debug products}-->
    {#if products.length === 0}
        <p>No products were added yet!</p>
    {:else}
        {#each products as product}
            <Product
                    productTitle={product.title}
                    productPrice={product.price}
                    productDescription={product.description}
                    on:addcart={addToCart} />
        {/each}
    {/if}
</section>
