<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SS Collection Nagpur</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">

<style>
body{
font-family:Poppins,sans-serif;
margin:0;
background:#f6f8fb;
}

header{
background:#0b3d91;
color:white;
padding:20px;
text-align:center;
}

.tagline{
font-size:14px;
opacity:0.9;
}

.filters{
display:flex;
overflow:auto;
gap:10px;
padding:10px;
background:white;
position:sticky;
top:0;
z-index:10;
}

.filters button{
border:none;
background:#e3eafc;
padding:8px 12px;
border-radius:20px;
cursor:pointer;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
gap:15px;
padding:15px;
}

.card{
background:white;
padding:10px;
border-radius:12px;
box-shadow:0 4px 8px rgba(0,0,0,0.05);
text-align:center;
}

.card img{
width:100%;
border-radius:10px;
}

.add{
background:#0b3d91;
color:white;
border:none;
padding:8px;
border-radius:8px;
margin-top:5px;
cursor:pointer;
}

.cart-btn{
position:fixed;
bottom:20px;
right:20px;
background:#0b3d91;
color:white;
padding:15px;
border-radius:50%;
cursor:pointer;
}

.whatsapp{
position:fixed;
bottom:80px;
right:20px;
background:#25D366;
color:white;
padding:15px;
border-radius:50%;
text-decoration:none;
}

.modal{
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.5);
display:none;
justify-content:center;
align-items:center;
}

.modal-content{
background:white;
padding:20px;
width:90%;
max-height:90%;
overflow:auto;
border-radius:12px;
}
</style>
</head>

<body>

<header>
<h2>SS Collection Nagpur</h2>
<div class="tagline">Branded Product Store All in one Brands</div>
</header>

<div class="filters">
<button onclick="filter('all')">All</button>
<button onclick="filter('shoes')">Shoes</button>
<button onclick="filter('mens')">Mens Wear</button>
<button onclick="filter('clothes')">Clothes</button>
</div>

<div class="grid" id="products"></div>

<div class="cart-btn" onclick="openCart()">🛒 <span id="count">0</span></div>

<a class="whatsapp" href="https://wa.me/919688728678" target="_blank">💬</a>

<div class="modal" id="cartModal">
<div class="modal-content">
<h3>Your Cart</h3>
<div id="cartItems"></div>
<h3>Total ₹ <span id="total">0</span></h3>

<form action="https://formspree.io/f/YOUR_FORM_ID_HERE" method="POST" onsubmit="return prepareOrder()">
<input required placeholder="Name" name="Customer Name"><br><br>
<input required placeholder="Phone" name="Phone"><br><br>
<textarea required placeholder="Address" name="Address"></textarea><br><br>
<textarea placeholder="Instructions" name="Instructions"></textarea>

<input type="hidden" name="Order Details" id="orderDetails">
<input type="hidden" name="_replyto" id="replyEmail">

<br><br>
<button type="submit">Place Order</button>
</form>

<br>
<button onclick="closeCart()">Close</button>
</div>
</div>

<script>

let products=[
{name:"Puma Shoes",price:999,cat:"shoes",img:"https://i.ibb.co/1f8vzH99/IMG-20260302-184612-986.jpg"},
{name:"Puma Shoes White",price:999,cat:"shoes",img:"https://i.ibb.co/hxv7Lhnq/IMG-20260302-184558-756.jpg"},
{name:"Puma Black",price:999,cat:"shoes",img:"https://i.ibb.co/Xr7mddff/IMG-20260302-184558-761.jpg"},
{name:"Mens Shirt",price:799,cat:"mens",img:"https://i.ibb.co/1f8vzH99/IMG-20260302-184612-986.jpg"},
{name:"Mens Jeans",price:1199,cat:"mens",img:"https://i.ibb.co/hxv7Lhnq/IMG-20260302-184558-756.jpg"},
{name:"Tshirt",price:599,cat:"clothes",img:"https://i.ibb.co/Xr7mddff/IMG-20260302-184558-761.jpg"},
{name:"Sports Shoes",price:1299,cat:"shoes",img:"https://i.ibb.co/1f8vzH99/IMG-20260302-184612-986.jpg"},
{name:"Casual Wear",price:899,cat:"clothes",img:"https://i.ibb.co/hxv7Lhnq/IMG-20260302-184558-756.jpg"}
];

let cart=JSON.parse(localStorage.getItem("cart"))||[];

function render(list){
let html="";
list.forEach((p,i)=>{
html+=`
<div class="card">
<img src="${p.img}" loading="lazy" alt="${p.name}">
<h4>${p.name}</h4>
<p>₹${p.price}</p>
<button class="add" onclick="add(${i})">Add</button>
</div>`;
});
document.getElementById("products").innerHTML=html;
}

function filter(cat){
if(cat==="all") render(products);
else render(products.filter(p=>p.cat===cat));
}

function add(i){
cart.push(products[i]);
localStorage.setItem("cart",JSON.stringify(cart));
updateCount();
}

function updateCount(){
document.getElementById("count").innerText=cart.length;
}
updateCount();
render(products);

function openCart(){
document.getElementById("cartModal").style.display="flex";
showCart();
}

function closeCart(){
document.getElementById("cartModal").style.display="none";
}

function showCart(){
let html="";
let total=0;
cart.forEach((item,i)=>{
total+=item.price;
html+=`${item.name} - ₹${item.price} <br>`;
});
document.getElementById("cartItems").innerHTML=html;
document.getElementById("total").innerText=total;
}

function prepareOrder(){
let summary="";
let total=0;
cart.forEach(item=>{
summary+=`${item.name} - ₹${item.price}\n`;
total+=item.price;
});
summary+="Total: ₹"+total;

document.getElementById("orderDetails").value=summary;
localStorage.removeItem("cart");
alert("Order placed! SS Collection Nagpur will contact you.");
return true;
}

</script>
</body>
</html>
