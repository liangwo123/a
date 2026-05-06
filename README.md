<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shop Dark</title>

<style>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont;
  background: #0f172a;
  color: #e5e7eb;
}

header {
  display: flex;
  justify-content: space-between;
  padding: 20px 40px;
  background: rgba(15,23,42,0.8);
  backdrop-filter: blur(10px);
}

.logo {
  font-size: 20px;
  font-weight: bold;
}

.cart {
  cursor: pointer;
}

.hero {
  text-align: center;
  padding: 100px 20px;
}

.hero h1 {
  font-size: 48px;
}

.products {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px,1fr));
  gap: 20px;
  padding: 40px;
}

.card {
  background: #1e293b;
  padding: 20px;
  border-radius: 12px;
  text-align: center;
}

button {
  background: #3b82f6;
  border: none;
  padding: 10px 20px;
  color: white;
  border-radius: 8px;
  cursor: pointer;
}

.cart-panel {
  position: fixed;
  right: 0;
  top: 0;
  width: 300px;
  height: 100%;
  background: #020617;
  padding: 20px;
  display: none;
}

</style>
</head>

<body>

<header>
  <div class="logo">My Store</div>
  <div class="cart" onclick="toggleCart()">
    🛒 <span id="count">0</span>
  </div>
</header>

<section class="hero">
  <h1>极简深色电商</h1>
  <p>高级、干净、现代</p>
</section>

<section class="products">

<div class="card">
  <h3>产品 A</h3>
  <p>¥99</p>
  <button onclick="addToCart('产品 A',99)">加入购物车</button>
</div>

<div class="card">
  <h3>产品 B</h3>
  <p>¥199</p>
  <button onclick="addToCart('产品 B',199)">加入购物车</button>
</div>

<div class="card">
  <h3>产品 C</h3>
  <p>¥299</p>
  <button onclick="addToCart('产品 C',299)">加入购物车</button>
</div>

</section>

<div class="cart-panel" id="cartPanel">
  <h2>购物车</h2>
  <div id="cartItems"></div>
</div>

<script>
let cart = JSON.parse(localStorage.getItem("cart")) || [];

function addToCart(name, price) {
  cart.push({name, price});
  localStorage.setItem("cart", JSON.stringify(cart));
  updateCart();
}

function updateCart() {
  document.getElementById("count").innerText = cart.length;

  let html = "";
  cart.forEach(item => {
    html += `<p>${item.name} - ¥${item.price}</p>`;
  });

  document.getElementById("cartItems").innerHTML = html;
}

function toggleCart() {
  let panel = document.getElementById("cartPanel");
  panel.style.display = panel.style.display === "block" ? "none" : "block";
}

updateCart();
</script>

</body>
</html>
