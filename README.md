- 👋 Hi, I’m @Attracx
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Attracx/Attracx is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple E-commerce Store</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Welcome to My E-commerce Store</h1>
        <nav>
            <button id="shop-button">Shop</button>
            <button id="cart-button">Cart (<span id="cart-count">0</span>)</button>
        </nav>
    </header>

    <main>
        <section id="products" class="hidden">
            <h2>Products</h2>
            <div class="product" data-id="1" data-name="Product 1" data-price="10">
                <h3>Product 1</h3>
                <p>Price: $10</p>
                <button class="add-to-cart">Add to Cart</button>
            </div>
            <div class="product" data-id="2" data-name="Product 2" data-price="20">
                <h3>Product 2</h3>
                <p>Price: $20</p>
                <button class="add-to-cart">Add to Cart</button>
            </div>
            <!-- और उत्पाद जोड़ें -->
        </section>

        <section id="cart" class="hidden">
            <h2>Shopping Cart</h2>
            <ul id="cart-items"></ul>
            <p id="total">Total: $0</p>
        </section>
    </main>

    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f8f8f8;
}

header {
    background-color: #333;
    color: #fff;
    padding: 10px 0;
    text-align: center;
}

nav {
    margin-top: 10px;
}

button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 10px;
    cursor: pointer;
    margin: 5px;
}

button:hover {
    background-color: #0056b3;
}

.hidden {
    display: none;
}

main {
    display: flex;
    justify-content: space-around;
    padding: 20px;
}

#products, #cart {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 45%;
}

.product {
    margin-bottom: 20px;
}

.add-to-cart {
    background-color: #28a745;
    color: #fff;
    border: none;
    padding: 10px;
    cursor: pointer;
}

.add-to-cart:hover {
    background-color: #218838;
}document.addEventListener('DOMContentLoaded', () => {
    let cart = JSON.parse(localStorage.getItem('cart')) || [];
    const cartItemsElement = document.getElementById('cart-items');
    const totalElement = document.getElementById('total');
    const cartCountElement = document.getElementById('cart-count');

    const shopButton = document.getElementById('shop-button');
    const cartButton = document.getElementById('cart-button');
    const productsSection = document.getElementById('products');
    const cartSection = document.getElementById('cart');

    shopButton.addEventListener('click', () => {
        productsSection.classList.remove('hidden');
        cartSection.classList.add('hidden');
    });

    cartButton.addEventListener('click', () => {
        productsSection.classList.add('hidden');
        cartSection.classList.remove('hidden');
    });

    document.querySelectorAll('.add-to-cart').forEach(button => {
        button.addEventListener('click', () => {
            const productElement = button.closest('.product');
            const product = {
                id: productElement.getAttribute('data-id'),
                name: productElement.getAttribute('data-name'),
                price: parseFloat(productElement.getAttribute('data-price'))
            };
            addToCart(product);
        });
    });

    function addToCart(product) {
        cart.push(product);
        saveCart();
        renderCart();
        updateCartCount();
    }

    function saveCart() {
        localStorage.setItem('cart', JSON.stringify(cart));
    }

    function renderCart() {
        cartItemsElement.innerHTML = '';
        let total = 0;
        cart.forEach((item, index) => {
            total += item.price;
            const li = document.createElement('li');
            li.textContent = `${item.name} - $${item.price}`;
            cartItemsElement.appendChild(li);
        });
        totalElement.textContent = `Total: $${total}`;
    }

    function updateCartCount() {
        cartCountElement.textContent = cart.length;
    }

    // Initial render
    renderCart();
    updateCartCount();
});
