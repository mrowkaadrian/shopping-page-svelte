<script>

    let guid = 1;
    let cart = [];
    const products = [
        {id: guid++, name: "Apple", image: "assets/apple.png", price: 1},
        {id: guid++, name: "Banana", image: "assets/banana.png", price: 2},
        {id: guid++, name: "Orange", image: "assets/orange.png", price: 3}
    ];
    $: total_price = cart.reduce((sum, item) => sum + item.price * item.quantity, 0)

    const addToCart = (product) => {
        let cartProduct = {
            ...product,
            quantity: 1
        }
        for (let item of cart) {
            if (item.id === product.id) {
                item.quantity++;
                cart = cart;
                return
            }
        }
        cart = [...cart, cartProduct]
    }

    const incrementAmount = (product) => {
        addToCart(product);
    }

    const decrementAmount = (product) => {
        for (let item of cart) {
            if (item.id === product.id) {
                if (--item.quantity === 0)
                    removeItemFromCart(product)
                cart = cart;
                console.log(products);
                return;
            }
        }
        console.log(products);
    }

    const removeItemFromCart = (product) => {
        cart = cart.filter(item => item.id !== product.id);
    }

</script>

<main>
    <div class="product-list">
        {#each products as product}
            <div class="product">
                <img src="{product.image}"  alt="{product.name}"/>
                <h4>{product.name}</h4>
                <p>{product.price}$</p>
                <button on:click={() => addToCart(product)}>Add to cart</button>
            </div>
        {/each}
    </div>

    <h1>Cart</h1>

    <div class="cart-list">
        {#each cart as item}
            <div class="cart-item">
                <img class="cart-item-details" src="{item.image}"  alt="{item.name}"/>
                <div class="cart-item-details">
                    {item.quantity}
                    <button on:click={() => decrementAmount(item)}>-</button>
                    <button on:click={() => incrementAmount(item)}>+</button>
                </div>
                <p class="cart-item-details">{item.price * item.quantity}$</p>
            </div>
        {/each}
        <div class="cart-total">
            <h4> Total: {total_price}$ </h4>
        </div>
    </div>
</main>

<style>
    .product-list, .cart-item {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
    }

    .cart-list {
        border: 2px solid #1a1a1a;
        padding: 1em;
    }

    .cart-total {
        text-align: right;
    }

    .cart-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 100%;
    }

    img {
        margin: 5px;
        height: 150px;
        width: 150px;
        background-size: contain;
        background-position: center;
        background-repeat: no-repeat;
    }
</style>
