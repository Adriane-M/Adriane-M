
[Uploa<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>A.D Clothing</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    html { scroll-behavior: smooth; }
    .hidden { display: none; }
    .product-container { 
      display: grid; 
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); 
      gap: 1rem;
    }
    .product { 
      background-color: white; 
      border-radius: 0.5rem; 
      box-shadow: 0 2px 8px rgba(0,0,0,0.1); 
      padding: 1rem; 
      text-align: center; 
    }
    .product img { 
      width: 100%; 
      height: auto; 
      border-radius: 0.5rem; 
      transition: transform 0.3s; 
    }
    .product:hover img { 
      transform: scale(1.05); 
    }
  </style>
</head>
<body class="bg-gray-100 text-gray-800">

  <header class="bg-gray-900 text-white text-center py-4">
    <h1 class="text-2xl font-bold">A.D Clothing</h1>
    <p>Your one-stop shop for stylish and comfy T-shirts!</p>
  </header>

  <nav class="bg-gray-700 text-white text-center py-3">
    <ul class="flex justify-center flex-wrap gap-4">
      <li><button onclick="showSection('shop'); changeTheme('women'); filterProducts('women')" class="hover:underline">Women</button></li>
      <li><button onclick="showSection('shop'); changeTheme('men'); filterProducts('men')" class="hover:underline">Men</button></li>
      <li><button onclick="showSection('shop'); changeTheme('kids'); filterProducts('kids')" class="hover:underline">Kids</button></li>
      <li><button onclick="showSection('cart')" class="hover:underline">Cart</button></li>
      <li><button onclick="showSection('checkout')" class="hover:underline">Checkout</button></li>
      <li><button onclick="showSection('contact')" class="hover:underline">Contact</button></li>
    </ul>
  </nav>

  <main class="p-4">
    <section id="shop">
      <h2 class="text-xl font-bold mb-4">Products</h2>
      <div id="product-container" class="product-container"></div>
    </section>

    <section id="cart" class="hidden">
      <h2 class="text-xl font-bold mb-4">Your Cart</h2>
      <div id="cart-items" class="space-y-4"></div>
      <p class="mt-4 font-semibold">Total: $<span id="cart-total">0</span></p>
      <button onclick="showSection('checkout')" class="mt-4 bg-green-600 text-white px-4 py-2 rounded">Checkout</button>
    </section>

    <section id="checkout" class="hidden">
      <h2 class="text-xl font-bold mb-4">Checkout</h2>
      <p>Checkout page content goes here.</p>
    </section>

    <section id="contact" class="hidden">
      <h2 class="text-xl font-bold mb-4">Contact Us</h2>
      <form class="space-y-4 max-w-md">
        <input type="text" placeholder="Name" class="w-full p-2 border border-gray-300 rounded" required />
        <input type="email" placeholder="Email" class="w-full p-2 border border-gray-300 rounded" required />
        <textarea placeholder="Message" class="w-full p-2 border border-gray-300 rounded" required></textarea>
        <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded">Send</button>
      </form>
    </section>
  </main>

  <footer class="bg-gray-900 text-white text-center py-4">
    <p>© 2025 A.D Clothing. All rights reserved.</p>
  </footer>

  <script>
    const products = {
      women: [
        {
          name: "Essentials Crop Tee",
          desc: "Chic & trendy streetwear inspired by Essentials.",
          price: 20,
          images: [
            "https://i.imgur.com/FzF1y0D.jpg",
            "https://i.imgur.com/VZcwPHH.gif"
          ]
        },
        {
          name: "HighMinds Oversized Tee",
          desc: "Soft oversized tee with streetwear vibes.",
          price: 22,
          images: [
            "https://i.imgur.com/IL8g0Y7.jpg",
            "https://i.imgur.com/E1Q7RUy.gif"
          ]
        },
        {
          name: "Hype Basic Tee",
          desc: "Comfortable and clean basic wear.",
          price: 18,
          images: [
            "https://i.imgur.com/QMiV8Dc.jpg",
            "https://i.imgur.com/l7ciwbW.gif"
          ]
        }
      ],
      men: [
        {
          name: "Don’t Blame the Kids Tee",
          desc: "Sleek and dope prints from DBTK.",
          price: 19,
          images: [
            "https://i.imgur.com/qMcezMf.jpg",
            "https://i.imgur.com/DXzM8y2.gif"
          ]
        },
        {
          name: "Skoop Graphic Tee",
          desc: "Eye-catching art and comfort in one.",
          price: 23,
          images: [
            "https://i.imgur.com/9myamE5.jpg",
            "https://i.imgur.com/AwFUnyZ.gif"
          ]
        },
        {
          name: "Local Loco V-Neck",
          desc: "Bold & classic V-neck from Local Loco.",
          price: 21,
          images: [
            "https://i.imgur.com/ZKBiK2O.jpg",
            "https://i.imgur.com/rMphOQG.gif"
          ]
        }
      ],
      kids: [
        {
          name: "Team Manila Kids Tee",
          desc: "Pinoy pride for the little ones.",
          price: 15,
          images: [
            "https://i.imgur.com/FQZg7UW.jpg",
            "https://i.imgur.com/p6KbXGE.gif"
          ]
        },
        {
          name: "Hiraya Cartoon Tee",
          desc: "Fun & Filipino-themed prints for kids.",
          price: 17,
          images: [
            "https://i.imgur.com/hG7JXYI.jpg",
            "https://i.imgur.com/NwsR36i.gif"
          ]
        },
        {
          name: "Island Kids Tee",
          desc: "Lightweight and ready for summer.",
          price: 14,
          images: [
            "https://i.imgur.com/njKMiXG.jpg",
            "https://i.imgur.com/OYGOsKb.gif"
          ]
        }
      ]
    };

    let cart = [];

    function showSection(id) {
      document.querySelectorAll("section").forEach(s => s.classList.add("hidden"));
      document.getElementById(id).classList.remove("hidden");
    }

    function changeTheme(category) {
      const body = document.querySelector("body");
      
      // Remove all previous background classes
      body.classList.remove("bg-pink-100", "bg-blue-100", "bg-green-100");
      
      if (category === 'women') {
        body.classList.add("bg-pink-100");
      } else if (category === 'men') {
        body.classList.add("bg-blue-100");
      } else if (category === 'kids') {
        body.classList.add("bg-green-100");
      }
    }

    function filterProducts(category) {
      const container = document.getElementById("product-container");
      container.innerHTML = "";
      products[category].forEach((p, index) => {
        const sliderId = `slider-${category}-${index}`;
        container.innerHTML += `
          <div class="product">
            <div class="relative overflow-hidden h-48 mb-3 rounded">
              <img id="${sliderId}" src="${p.images[0]}" alt="${p.name}" class="w-full h-48 object-cover transition-all duration-500">
            </div>
            <h3 class="font-bold">${p.name}</h3>
            <p>${p.desc}</p>
            <p class="font-semibold mt-2">$${p.price}</p>

            <!-- Size Dropdown -->
            <label for="size" class="block mt-2">Select Size:</label>
            <select id="size-${category}-${index}" class="w-full p-2 border border-gray-300 rounded mb-2">
              <option value="S">Small</option>
              <option value="M">Medium</option>
              <option value="L">Large</option>
              <option value="XL">X-Large</option>
            </select>

            <button onclick="addToCart('${category}', ${index})" class="mt-2 bg-blue-600 text-white px-4 py-1 rounded">Add to Cart</button>
            <button onclick="showSection('checkout')" class="ml-2 mt-2 bg-green-600 text-white px-4 py-1 rounded">Buy Now</button>
          </div>`;
        startAutoSlide(sliderId, p.images);
      });
    }

    function startAutoSlide(id, images) {
      let i = 0;
      setInterval(() => {
        i = (i + 1) % images.length;
        const img = document.getElementById(id);
        if (img) img.src = images[i];
      }, 3000);
    }

    function addToCart(category, index) {
      const item = products[category][index];
      const size = document.getElementById(`size-${category}-${index}`).value;
      const cartItem = {
        ...item,
        size,
        qty: 1
      };
      
      const existing = cart.find(p => p.name === item.name && p.size === size);
      if (existing) {
        existing.qty++;
      } else {
        cart.push(cartItem);
      }
      updateCart();
      showSection('cart');
    }

    function updateCart() {
      const cartItems = document.getElementById("cart-items");
      const total = document.getElementById("cart-total");
      cartItems.innerHTML = "";
      let sum = 0;

      cart.forEach((item, i) => {
        sum += item.price * item.qty;
        cartItems.innerHTML += `
          <div class="bg-white p-4 rounded shadow flex justify-between items-center">
            <div>
              <h4 class="font-bold">${item.name} - Size: ${item.size}</h4>
              <p>$${item.price} x ${item.qty}</p>
            </div>
            <div class="flex items-center gap-2">
              <button onclick="changeQty(${i}, -1)" class="bg-gray-300 px-2 rounded">-</button>
              <span>${item.qty}</span>
              <button onclick="changeQty(${i}, 1)" class="bg-gray-300 px-2 rounded">+</button>
              <button onclick="removeFromCart(${i})" class="bg-red-500 text-white px-2 rounded">Remove</button>
            </div>
          </div>`;
      });

      total.textContent = sum.toFixed(2);
    }

    function changeQty(index, delta) {
      cart[index].qty += delta;
      if (cart[index].qty <= 0) cart.splice(index, 1);
      updateCart();
    }

    function removeFromCart(index) {
      cart.splice(index, 1);
      updateCart();
    }

    // Load initial
    showSection('shop');
    changeTheme('women');
    filterProducts('women');
  </script>

</body>
</html>
ding A.D CLOTHING_transfer_2025-04-07_073427.html…]()
