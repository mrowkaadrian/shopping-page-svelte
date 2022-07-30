<script>
    let guid = 1;
    let cart = [];
    let products = [
        {id: guid++, name: "Apple", image: "assets/apple.jpg", price: 1, quantity: 1},
        {id: guid++, name: "Banana", image: "assets/banana.jpg", price: 2, quantity: 1},
        {id: guid++, name: "Orange", image: "assets/orange.jpg", price: 3, quantity: 1}
    ];

    const addToCart = (product) => {
        for (let item of cart) {
            if (item.id === product.id) {
                item.quantity++;
                cart = cart;
                return
            }
        }
        cart = [...cart, product]
    }
</script>

<main>
    <div class="product-list">
        {#each products as product}
            <div class="product">
                <img src="{product.image}">
                <h4>{product.name}</h4>
                <p>{product.price}$</p>
                <button on:click={() => addToCart(product)}>Add to cart</button>
            </div>
        {/each}
    </div>
    Cart: {JSON.stringify(cart)}
</main>

<style>
    .product-list {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
    }

    img {
        height: 150px;
        width: 150px;
        background-size: contain;
        background-position: center;
        background-repeat: no-repeat;
    }
</style>
