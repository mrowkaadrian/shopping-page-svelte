<script>
    let products = [
        {name: "Apple", image: "assets/apple.jpg", price: 1},
        {name: "Banana", image: "assets/banana.jpg", price: 2},
        {name: "Orange", image: "assets/orange.jpg", price: 3}
    ];
</script>

<main>
    <div class="product-list">
        {#each products as product}
            <div class="product">
                <img src="{product.image}">
                <h4>{product.name}</h4>
                <p>{product.price}$</p>
                <button>Add to cart</button>
            </div>
        {/each}
    </div>
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
