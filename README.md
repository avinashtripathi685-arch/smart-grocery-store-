<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Abhinash Grocery Store</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0;}
:root{
  --green:#2e7d32;--green-light:#43a047;--green-pale:#e8f5e9;
  --accent:#ff6f00;--bg:#f0f4f0;--text:#1b1b1b;--muted:#777;
  --radius:14px;--shadow:0 4px 18px rgba(0,0,0,0.08);
}
body{font-family:'Nunito',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;}
.header{background:linear-gradient(135deg,var(--green),var(--green-light));color:white;padding:16px 18px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100;box-shadow:0 3px 15px rgba(46,125,50,0.3);}
.header h1{font-size:1.35rem;font-weight:900;}
.cart-badge{background:var(--accent);color:white;font-size:0.78rem;font-weight:800;padding:5px 12px;border-radius:20px;cursor:pointer;transition:transform 0.2s;display:flex;align-items:center;gap:5px;}
.cart-badge:hover{transform:scale(1.08);}
.search-wrap{padding:14px 15px 6px;}
.search-wrap input{width:100%;padding:11px 18px;border:2px solid #ddd;border-radius:30px;font-size:0.95rem;font-family:'Nunito',sans-serif;outline:none;transition:border 0.2s;background:white;}
.search-wrap input:focus{border-color:var(--green);}
.categories{display:flex;gap:8px;padding:8px 15px 10px;overflow-x:auto;scrollbar-width:none;}
.categories::-webkit-scrollbar{display:none;}
.cat-btn{padding:6px 15px;border-radius:20px;border:2px solid #ddd;background:white;font-family:'Nunito',sans-serif;font-weight:700;font-size:0.82rem;cursor:pointer;white-space:nowrap;transition:all 0.2s;color:var(--muted);}
.cat-btn.active{background:var(--green);border-color:var(--green);color:white;}
.section-title{padding:6px 15px 4px;font-size:0.82rem;font-weight:800;color:var(--muted);text-transform:uppercase;letter-spacing:1px;}
.container{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:12px;padding:10px 15px 100px;}
.parent-card{background:white;border-radius:var(--radius);overflow:hidden;box-shadow:var(--shadow);display:flex;flex-direction:column;align-items:center;cursor:pointer;transition:transform 0.2s,box-shadow 0.2s;border:2px solid transparent;}
.parent-card:hover{transform:translateY(-3px);box-shadow:0 8px 25px rgba(0,0,0,0.12);}
.parent-card.expanded{border-color:var(--green);}
.parent-img-wrap{width:100%;height:100px;overflow:hidden;}
.parent-img-wrap img{width:100%;height:100%;object-fit:cover;transition:transform 0.4s;}
.parent-card:hover .parent-img-wrap img{transform:scale(1.07);}
.parent-info{padding:10px 10px 12px;width:100%;display:flex;flex-direction:column;align-items:center;gap:4px;}
.parent-name{font-weight:800;font-size:0.88rem;text-align:center;}
.parent-sub-count{font-size:0.72rem;color:var(--muted);font-weight:700;background:#f0f0f0;padding:2px 8px;border-radius:10px;}
.parent-card.expanded .parent-sub-count{background:var(--green);color:white;}
.expand-arrow{font-size:0.72rem;color:var(--muted);transition:transform 0.3s;}
.parent-card.expanded .expand-arrow{transform:rotate(180deg);color:var(--green);}
.sub-panel{grid-column:1/-1;background:white;border-radius:var(--radius);box-shadow:var(--shadow);overflow:hidden;max-height:0;transition:max-height 0.45s ease,padding 0.3s;border-left:4px solid var(--green);}
.sub-panel.open{max-height:4000px;padding:16px;}
.sub-panel-title{font-size:0.8rem;font-weight:800;color:var(--green);text-transform:uppercase;letter-spacing:1px;margin-bottom:12px;}
.sub-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(130px,1fr));gap:10px;}
.sub-item{background:#fafafa;border-radius:10px;overflow:hidden;display:flex;flex-direction:column;align-items:center;transition:transform 0.15s;border:1px solid #eee;}
.sub-item:hover{transform:translateY(-2px);box-shadow:0 4px 12px rgba(0,0,0,0.1);}
.sub-img-wrap{width:100%;height:80px;overflow:hidden;}
.sub-img-wrap img{width:100%;height:100%;object-fit:cover;transition:transform 0.3s;}
.sub-item:hover .sub-img-wrap img{transform:scale(1.08);}
.sub-info{padding:8px 8px 6px;width:100%;display:flex;flex-direction:column;align-items:center;gap:3px;}
.sub-brand{background:var(--green-pale);color:var(--green);font-size:0.65rem;font-weight:900;padding:2px 8px;border-radius:8px;text-align:center;max-width:100%;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.sub-item-name{font-weight:800;font-size:0.78rem;text-align:center;line-height:1.2;}
.sub-item-price{color:var(--green);font-weight:900;font-size:0.88rem;}
.sub-item-unit{font-size:0.68rem;color:var(--muted);font-weight:600;}
.qty-row{display:flex;align-items:center;gap:5px;margin-top:2px;}
.qty-row button{width:26px;height:26px;border-radius:50%;border:none;background:var(--green-pale);color:var(--green);font-size:1rem;font-weight:900;cursor:pointer;transition:background 0.15s;line-height:1;}
.qty-row button:hover{background:var(--green);color:white;}
.qty-row span{font-weight:800;font-size:0.9rem;min-width:18px;text-align:center;}
.add-sub-btn{width:100%;padding:7px;background:var(--green);color:white;border:none;border-radius:0 0 8px 8px;font-family:'Nunito',sans-serif;font-weight:800;font-size:0.78rem;cursor:pointer;transition:background 0.15s;margin-top:4px;}
.add-sub-btn:hover{background:var(--green-light);}
.add-sub-btn.in-cart{background:var(--accent);}
.cart-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.4);z-index:200;}
.cart-overlay.open{display:block;}
.cart-drawer{position:fixed;bottom:0;left:0;right:0;background:white;border-radius:22px 22px 0 0;padding:20px 18px;max-height:80vh;overflow-y:auto;z-index:300;transform:translateY(100%);transition:transform 0.35s cubic-bezier(.4,0,.2,1);box-shadow:0 -8px 30px rgba(0,0,0,0.15);}
.cart-drawer.open{transform:translateY(0);}
.drawer-handle{width:40px;height:4px;background:#ddd;border-radius:4px;margin:0 auto 18px;}
.cart-drawer h2{font-size:1.2rem;font-weight:900;margin-bottom:14px;}
.cart-item{display:flex;align-items:center;justify-content:space-between;padding:10px 0;border-bottom:1px solid #f0f0f0;}
.cart-item-name{font-weight:700;font-size:0.9rem;}
.cart-item-sub{color:var(--muted);font-size:0.78rem;}
.cart-qty{display:flex;align-items:center;gap:5px;}
.cart-qty button{width:26px;height:26px;border-radius:50%;border:none;background:var(--green-pale);color:var(--green);font-weight:900;font-size:1rem;cursor:pointer;}
.cart-qty button:hover{background:var(--green);color:white;}
.cart-qty span{font-weight:800;min-width:18px;text-align:center;}
.remove-btn{background:none;border:none;color:#e53935;font-size:1.1rem;cursor:pointer;padding:4px;}
.cart-footer{margin-top:14px;}
.total-row{display:flex;justify-content:space-between;font-size:1.1rem;font-weight:900;margin-bottom:14px;}
.total-row span:last-child{color:var(--green);}
.btn-row{display:flex;gap:10px;}
.clear-btn{flex:1;padding:12px;background:#ffebee;color:#e53935;border:none;border-radius:10px;font-family:'Nunito',sans-serif;font-weight:800;font-size:0.92rem;cursor:pointer;}
.order-btn{flex:2;padding:12px;background:linear-gradient(135deg,#25d366,#128c7e);color:white;border:none;border-radius:10px;font-family:'Nunito',sans-serif;font-weight:800;font-size:0.92rem;cursor:pointer;}
.empty-cart{text-align:center;padding:30px 0;color:var(--muted);}
.empty-cart div{font-size:2.5rem;margin-bottom:8px;}
.toast{position:fixed;bottom:90px;left:50%;transform:translateX(-50%) translateY(20px);background:#323232;color:white;padding:10px 22px;border-radius:25px;font-weight:700;font-size:0.88rem;opacity:0;transition:all 0.3s;z-index:400;pointer-events:none;white-space:nowrap;}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0);}
.float-cart{position:fixed;bottom:20px;left:50%;transform:translateX(-50%);background:var(--green);color:white;border:none;border-radius:30px;padding:13px 26px;font-family:'Nunito',sans-serif;font-weight:800;font-size:1rem;cursor:pointer;box-shadow:0 6px 20px rgba(46,125,50,0.4);display:flex;align-items:center;gap:8px;z-index:100;transition:transform 0.2s;}
.float-cart:hover{transform:translateX(-50%) translateY(-2px);}
.float-cart.hidden{display:none;}
.no-results{grid-column:1/-1;text-align:center;padding:40px;color:var(--muted);font-weight:700;}
</style>
</head>
<body>
 
<div class="header">
  <h1>🛒 Avinash Store</h1>
  <div class="cart-badge" onclick="openCart()">🛒 Cart <span id="cart-count">0</span></div>
</div>
<div class="search-wrap">
  <input type="text" id="search" placeholder="🔍 Search item or brand..." oninput="renderAll()">
</div>
<div class="categories" id="categories"></div>
<div class="section-title" id="section-label">All Products</div>
<div class="container" id="products"></div>
<button class="float-cart hidden" id="float-cart-btn" onclick="openCart()">🛒 View Cart · ₹<span id="float-total">0</span></button>
<div class="cart-overlay" id="cart-overlay" onclick="closeCart()"></div>
<div class="cart-drawer" id="cart-drawer">
  <div class="drawer-handle"></div>
  <h2>Your Cart 🛒</h2>
  <div id="cart-items"></div>
  <div class="cart-footer" id="cart-footer"></div>
</div>
<div class="toast" id="toast"></div>
 
<script>
const I = 'https://images.unsplash.com/photo-';
const catalog = [
  // ══ GRAINS ══
  { id:'rice', name:'Rice', cat:'Grains', img:I+'1586201375761-83865001e31c?w=400&q=80', types:[
    {brand:'India Gate', name:'Classic Basmati',    price:180,unit:'1kg/500gm', img:I+'1586201375761-83865001e31c?w=300&q=80'},
    {brand:'India Gate', name:'Super Basmati',      price:220,unit:'1kg/500gm', img:I+'1586201375761-83865001e31c?w=300&q=80'},
    {brand:'Daawat',     name:'Rozana Basmati',     price:150,unit:'1kg/500gm', img:I+'1586201375761-83865001e31c?w=300&q=80'},
    {brand:'Daawat',     name:'Biryani Basmati',    price:200,unit:'1kg/500gm', img:I+'1586201375761-83865001e31c?w=300&q=80'},
    {brand:'Kohinoor',   name:'Basmati Rice',       price:160,unit:'1kg/500gm', img:I+'1586201375761-83865001e31c?w=300&q=80'},
    {brand:'Fortune',    name:'Basmati Rice',       price:130,unit:'1kg/500gm', img:I+'1586201375761-83865001e31c?w=300&q=80'},
    {brand:'Patanjali',  name:'Basmati Rice',       price:120,unit:'1kg/500gm', img:I+'1586201375761-83865001e31c?w=300&q=80'},
    {brand:'24 Mantra',  name:'Organic Brown Rice', price:180,unit:'1kg/500gm', img:I+'1536304993881-ff86e0c9a28c?w=300&q=80'},
    {brand:'Local',      name:'Sona Masoori',       price:80, unit:'1kg/500gm', img:I+'1536304993881-ff86e0c9a28c?w=300&q=80'},
    {brand:'Local',      name:'Idli Rice',          price:65, unit:'1kg/500gm', img:I+'1536304993881-ff86e0c9a28c?w=300&q=80'},
    {brand:'Local',      name:'Parboiled Rice',     price:70, unit:'1kg/500gm', img:I+'1536304993881-ff86e0c9a28c?w=300&q=80'},
  ]},
  { id:'flour', name:'Flour', cat:'Grains', img:I+'1574323347407-f5e1ad6d020b?w=400&q=80', types:[
    {brand:'Aashirvaad', name:'Whole Wheat Atta',   price:58, unit:'1kg', img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
    {brand:'Aashirvaad', name:'Multigrain Atta',    price:75, unit:'1kg', img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
    {brand:'Pillsbury',  name:'Chakki Fresh Atta',  price:52, unit:'1kg', img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
    {brand:'Fortune',    name:'Chakki Atta',        price:50, unit:'1kg', img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
    {brand:'Patanjali',  name:'Wheat Flour',        price:44, unit:'1kg', img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
    {brand:'Rajdhani',   name:'Besan',              price:90, unit:'500g',img:I+'1612257416648-f4e773b4f073?w=300&q=80'},
    {brand:'Patanjali',  name:'Besan',              price:80, unit:'500g',img:I+'1612257416648-f4e773b4f073?w=300&q=80'},
    {brand:'Local',      name:'Maida',              price:40, unit:'1kg', img:I+'1558618666-fcd25c85cd64?w=300&q=80'},
    {brand:'Local',      name:'Ragi Flour',         price:80, unit:'500g',img:I+'1603569283847-aa295f0d016a?w=300&q=80'},
    {brand:'Local',      name:'Jowar Flour',        price:60, unit:'500g',img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
    {brand:'Local',      name:'Bajra Flour',        price:50, unit:'500g',img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
    {brand:'Catch',      name:'Corn Flour',         price:55, unit:'500g',img:I+'1551754655-cd27e38d2076?w=300&q=80'},
    {brand:'MTR',        name:'Sooji (Semolina)',   price:38, unit:'500g',img:I+'1574323347407-f5e1ad6d020b?w=300&q=80'},
  ]},
  { id:'dal', name:'Dal & Pulses', cat:'Grains', img:I+'1612257416648-f4e773b4f073?w=400&q=80', types:[
    {brand:'Tata Sampann',name:'Toor Dal',          price:145,unit:'1kg', img:I+'1612257416648-f4e773b4f073?w=300&q=80'},
    {brand:'Patanjali',  name:'Toor Dal',           price:130,unit:'1kg', img:I+'1612257416648-f4e773b4f073?w=300&q=80'},
    {brand:'Tata Sampann',name:'Moong Dal',         price:135,unit:'1kg', img:I+'1596797038530-2c107229654b?w=300&q=80'},
    {brand:'Local',      name:'Moong Dal',          price:120,unit:'1kg', img:I+'1596797038530-2c107229654b?w=300&q=80'},
    {brand:'Tata Sampann',name:'Chana Dal',         price:110,unit:'1kg', img:I+'1585664811087-47f65abbad64?w=300&q=80'},
    {brand:'Rajdhani',   name:'Chana Dal',          price:100,unit:'1kg', img:I+'1585664811087-47f65abbad64?w=300&q=80'},
    {brand:'Tata Sampann',name:'Masoor Dal',        price:105,unit:'1kg', img:I+'1612257416648-f4e773b4f073?w=300&q=80'},
    {brand:'Local',      name:'Masoor Dal',         price:95, unit:'1kg', img:I+'1612257416648-f4e773b4f073?w=300&q=80'},
    {brand:'Tata Sampann',name:'Urad Dal White',    price:120,unit:'1kg', img:I+'1596797038530-2c107229654b?w=300&q=80'},
    {brand:'Local',      name:'Urad Dal Black',     price:115,unit:'1kg', img:I+'1596797038530-2c107229654b?w=300&q=80'},
    {brand:'Rajdhani',   name:'Kabuli Chana',       price:130,unit:'500g',img:I+'1585664811087-47f65abbad64?w=300&q=80'},
    {brand:'Local',      name:'Rajma Red',          price:140,unit:'500g',img:I+'1585664811087-47f65abbad64?w=300&q=80'},
    {brand:'Local',      name:'Rajma Jammu',        price:160,unit:'500g',img:I+'1585664811087-47f65abbad64?w=300&q=80'},
  ]},
  // ══ DAIRY ══
  { id:'milk', name:'Milk', cat:'Dairy', img:I+'1550583724-b2692b85b150?w=400&q=80', types:[
    {brand:'Amul',        name:'Full Cream Milk',   price:68, unit:'1L',  img:I+'1550583724-b2692b85b150?w=300&q=80'},
    {brand:'Amul',        name:'Toned Milk',        price:54, unit:'1L',  img:I+'1563636619-e9143da7973b?w=300&q=80'},
    {brand:'Amul',        name:'Double Toned',      price:48, unit:'1L',  img:I+'1563636619-e9143da7973b?w=300&q=80'},
    {brand:'Amul',        name:'UHT Milk',          price:75, unit:'1L',  img:I+'1550583724-b2692b85b150?w=300&q=80'},
    {brand:'Mother Dairy',name:'Full Cream Milk',   price:65, unit:'1L',  img:I+'1550583724-b2692b85b150?w=300&q=80'},
    {brand:'Mother Dairy',name:'Toned Milk',        price:52, unit:'1L',  img:I+'1563636619-e9143da7973b?w=300&q=80'},
    {brand:'Parag',       name:'Full Cream Milk',   price:64, unit:'1L',  img:I+'1550583724-b2692b85b150?w=300&q=80'},
    {brand:'Verka',       name:'Full Cream Milk',   price:66, unit:'1L',  img:I+'1550583724-b2692b85b150?w=300&q=80'},
    {brand:'So Good',     name:'Soy Milk',          price:90, unit:'200ml',img:I+'1612257999046-49f65a0f8c68?w=300&q=80'},
    {brand:'So Good',     name:'Almond Milk',       price:120,unit:'200ml',img:I+'1612257999046-49f65a0f8c68?w=300&q=80'},
  ]},
  { id:'dairy2', name:'Curd & Paneer', cat:'Dairy', img:I+'1631452180519-c014fe946bc7?w=400&q=80', types:[
    {brand:'Amul',        name:'Fresh Curd',        price:48, unit:'400g',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Amul',        name:'Greek Yogurt',      price:85, unit:'200g',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Mother Dairy',name:'Fresh Curd',        price:42, unit:'400g',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Nestle',      name:'A+ Curd',           price:55, unit:'400g',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Amul',        name:'Paneer',            price:340,unit:'200g',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Verka',       name:'Paneer',            price:320,unit:'200g',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Mother Dairy',name:'Paneer',            price:330,unit:'200g',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Amul',        name:'Butter Salted',     price:58, unit:'100g',img:I+'1589985270826-4b7bb135bc9d?w=300&q=80'},
    {brand:'Amul',        name:'Butter Unsalted',   price:58, unit:'100g',img:I+'1589985270826-4b7bb135bc9d?w=300&q=80'},
    {brand:'Amul',        name:'Ghee',              price:285,unit:'500ml',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Patanjali',   name:'Ghee',              price:250,unit:'500ml',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Gowardhan',   name:'Ghee',              price:265,unit:'500ml',img:I+'1631452180519-c014fe946bc7?w=300&q=80'},
    {brand:'Amul',        name:'Cheese Slices',     price:95, unit:'200g',img:I+'1486297678162-eb2a19b0a32d?w=300&q=80'},
    {brand:'Amul',        name:'Cheese Spread',     price:110,unit:'180g',img:I+'1486297678162-eb2a19b0a32d?w=300&q=80'},
  ]},
  // ══ ESSENTIALS ══
  { id:'oil', name:'Cooking Oil', cat:'Essentials', img:I+'1474979266404-7eaacbcd87c5?w=400&q=80', types:[
    {brand:'Fortune',    name:'Sunflower Oil',      price:130,unit:'1L',  img:I+'1474979266404-7eaacbcd87c5?w=300&q=80'},
    {brand:'Saffola',    name:'Gold Sunflower Oil', price:160,unit:'1L',  img:I+'1474979266404-7eaacbcd87c5?w=300&q=80'},
    {brand:'Saffola',    name:'Total Heart Oil',    price:180,unit:'1L',  img:I+'1474979266404-7eaacbcd87c5?w=300&q=80'},
    {brand:'Patanjali',  name:'Mustard Oil',        price:140,unit:'1L',  img:I+'1599487488170-d11ec9c172f0?w=300&q=80'},
    {brand:'Engine',     name:'Kachi Ghani Mustard',price:158,unit:'1L',  img:I+'1599487488170-d11ec9c172f0?w=300&q=80'},
    {brand:'Dhara',      name:'Mustard Oil',        price:145,unit:'1L',  img:I+'1599487488170-d11ec9c172f0?w=300&q=80'},
    {brand:'Parachute',  name:'Coconut Oil',        price:200,unit:'1L',  img:I+'1526893412053-caf498060368?w=300&q=80'},
    {brand:'Dabur',      name:'Coconut Oil',        price:215,unit:'1L',  img:I+'1526893412053-caf498060368?w=300&q=80'},
    {brand:'Fortune',    name:'Groundnut Oil',      price:160,unit:'1L',  img:I+'1474979266404-7eaacbcd87c5?w=300&q=80'},
    {brand:'DiSano',     name:'Olive Oil',          price:350,unit:'500ml',img:I+'1596040033229-a9821ebd058d?w=300&q=80'},
    {brand:'Borges',     name:'Olive Oil',          price:390,unit:'500ml',img:I+'1596040033229-a9821ebd058d?w=300&q=80'},
    {brand:'Fortune',    name:'Rice Bran Oil',      price:135,unit:'1L',  img:I+'1474979266404-7eaacbcd87c5?w=300&q=80'},
  ]},
  { id:'spices', name:'Spices', cat:'Essentials', img:I+'1532336414038-cf19250c5757?w=400&q=80', types:[
    {brand:'Everest',    name:'Turmeric Powder',    price:32, unit:'100g',img:I+'1615485500704-8e990f9900f7?w=300&q=80'},
    {brand:'MDH',        name:'Turmeric Powder',    price:35, unit:'100g',img:I+'1615485500704-8e990f9900f7?w=300&q=80'},
    {brand:'Patanjali',  name:'Turmeric Powder',    price:28, unit:'100g',img:I+'1615485500704-8e990f9900f7?w=300&q=80'},
    {brand:'Everest',    name:'Red Chilli Powder',  price:42, unit:'100g',img:I+'1588514912908-b5a89578dc7f?w=300&q=80'},
    {brand:'MDH',        name:'Red Chilli Powder',  price:45, unit:'100g',img:I+'1588514912908-b5a89578dc7f?w=300&q=80'},
    {brand:'Everest',    name:'Coriander Powder',   price:28, unit:'100g',img:I+'1532336414038-cf19250c5757?w=300&q=80'},
    {brand:'MDH',        name:'Coriander Powder',   price:30, unit:'100g',img:I+'1532336414038-cf19250c5757?w=300&q=80'},
    {brand:'Everest',    name:'Garam Masala',       price:55, unit:'100g',img:I+'1506368249639-73a05d6f6488?w=300&q=80'},
    {brand:'MDH',        name:'Garam Masala',       price:60, unit:'100g',img:I+'1506368249639-73a05d6f6488?w=300&q=80'},
    {brand:'MDH',        name:'Kitchen King Masala',price:62, unit:'100g',img:I+'1506368249639-73a05d6f6488?w=300&q=80'},
    {brand:'Everest',    name:'Biryani Masala',     price:50, unit:'50g', img:I+'1532336414038-cf19250c5757?w=300&q=80'},
    {brand:'MDH',        name:'Chaat Masala',       price:42, unit:'100g',img:I+'1506368249639-73a05d6f6488?w=300&q=80'},
    {brand:'Catch',      name:'Black Pepper',       price:65, unit:'50g', img:I+'1506368249639-73a05d6f6488?w=300&q=80'},
    {brand:'Local',      name:'Cumin (Jeera)',      price:35, unit:'100g',img:I+'1599487488170-d11ec9c172f0?w=300&q=80'},
    {brand:'Local',      name:'Cardamom (Elaichi)', price:80, unit:'50g', img:I+'1532336414038-cf19250c5757?w=300&q=80'},
  ]},
  { id:'sugar_salt', name:'Sugar & Salt', cat:'Essentials', img:I+'1558642084-fd07fae5282e?w=400&q=80', types:[
    {brand:'Uttam',      name:'White Sugar',        price:50, unit:'1kg', img:I+'1558642084-fd07fae5282e?w=300&q=80'},
    {brand:'Local',      name:'White Sugar',        price:45, unit:'1kg', img:I+'1558642084-fd07fae5282e?w=300&q=80'},
    {brand:'Local',      name:'Brown Sugar',        price:80, unit:'500g',img:I+'1611241893603-3c359704e0ee?w=300&q=80'},
    {brand:'Local',      name:'Bura Sugar',         price:55, unit:'500g',img:I+'1558642084-fd07fae5282e?w=300&q=80'},
    {brand:'Patanjali',  name:'Jaggery Block',      price:65, unit:'500g',img:I+'1611241893603-3c359704e0ee?w=300&q=80'},
    {brand:'Local',      name:'Jaggery Powder',     price:70, unit:'500g',img:I+'1611241893603-3c359704e0ee?w=300&q=80'},
    {brand:'Tata',       name:'Iodised Salt',       price:22, unit:'1kg', img:I+'1584255014406-2a68ea38e48c?w=300&q=80'},
    {brand:'Catch',      name:'Iodised Salt',       price:20, unit:'1kg', img:I+'1584255014406-2a68ea38e48c?w=300&q=80'},
    {brand:'Patanjali',  name:'Sendha Namak',       price:30, unit:'500g',img:I+'1584255014406-2a68ea38e48c?w=300&q=80'},
    {brand:'Catch',      name:'Rock Salt',          price:35, unit:'500g',img:I+'1584255014406-2a68ea38e48c?w=300&q=80'},
    {brand:'Catch',      name:'Black Salt',         price:40, unit:'200g',img:I+'1584255014406-2a68ea38e48c?w=300&q=80'},
  ]},
  { id:'condiments', name:'Sauces & Jams', cat:'Essentials', img:I+'1472476443507-c7a5948772fc?w=400&q=80', types:[
    {brand:'Kissan',     name:'Tomato Ketchup',     price:120,unit:'500g',img:I+'1472476443507-c7a5948772fc?w=300&q=80'},
    {brand:'Maggi',      name:'Tomato Ketchup',     price:115,unit:'500g',img:I+'1472476443507-c7a5948772fc?w=300&q=80'},
    {brand:'Heinz',      name:'Tomato Ketchup',     price:160,unit:'500g',img:I+'1472476443507-c7a5948772fc?w=300&q=80'},
    {brand:'Maggi',      name:'Chilli Sauce',       price:90, unit:'200ml',img:I+'1588514912908-b5a89578dc7f?w=300&q=80'},
    {brand:'Chings',     name:'Green Chilli Sauce', price:80, unit:'200ml',img:I+'1588514912908-b5a89578dc7f?w=300&q=80'},
    {brand:'Kissan',     name:'Mixed Fruit Jam',    price:150,unit:'500g',img:I+'1563805042-7684c019e1cb?w=300&q=80'},
    {brand:'Kissan',     name:'Strawberry Jam',     price:160,unit:'500g',img:I+'1563805042-7684c019e1cb?w=300&q=80'},
    {brand:'Dabur',      name:'Honey',              price:220,unit:'500g',img:I+'1587049352846-4a222e784d38?w=300&q=80'},
    {brand:'Patanjali',  name:'Honey',              price:200,unit:'500g',img:I+'1587049352846-4a222e784d38?w=300&q=80'},
    {brand:'Sundrop',    name:'Peanut Butter Creamy',price:200,unit:'400g',img:I+'1558301211-0d8c8ddee6ec?w=300&q=80'},
    {brand:'Dr. Oetker', name:'Peanut Butter Crunchy',price:220,unit:'400g',img:I+'1558301211-0d8c8ddee6ec?w=300&q=80'},
    {brand:'Dr. Oetker', name:'Mayonnaise',         price:100,unit:'250g',img:I+'1472476443507-c7a5948772fc?w=300&q=80'},
  ]},
  // ══ BEVERAGES ══
  { id:'tea', name:'Tea', cat:'Beverages', img:I+'1556679343-c7306c1976bc?w=400&q=80', types:[
    {brand:'Tata',       name:'Tea Gold',           price:200,unit:'250g',  img:I+'1556679343-c7306c1976bc?w=300&q=80'},
    {brand:'Tata',       name:'Tea Premium',        price:180,unit:'250g',  img:I+'1556679343-c7306c1976bc?w=300&q=80'},
    {brand:'Brooke Bond',name:'Red Label Tea',      price:185,unit:'250g',  img:I+'1571934811356-5cc061b6821f?w=300&q=80'},
    {brand:'Brooke Bond',name:'Taaza Tea',          price:160,unit:'250g',  img:I+'1571934811356-5cc061b6821f?w=300&q=80'},
    {brand:'Wagh Bakri', name:'Premium Leaf Tea',   price:190,unit:'250g',  img:I+'1571934811356-5cc061b6821f?w=300&q=80'},
    {brand:'Wagh Bakri', name:'Masala Tea',         price:165,unit:'100g',  img:I+'1556679343-c7306c1976bc?w=300&q=80'},
    {brand:'Society',    name:'Premium Tea',        price:195,unit:'250g',  img:I+'1571934811356-5cc061b6821f?w=300&q=80'},
    {brand:'Lipton',     name:'Green Tea',          price:150,unit:'25 bags',img:I+'1627435601361-ec25f5b1d0e5?w=300&q=80'},
    {brand:'Tetley',     name:'Green Tea',          price:160,unit:'25 bags',img:I+'1627435601361-ec25f5b1d0e5?w=300&q=80'},
    {brand:'Twinings',   name:'Green Tea',          price:220,unit:'25 bags',img:I+'1627435601361-ec25f5b1d0e5?w=300&q=80'},
    {brand:'Patanjali',  name:'Tulsi Tea',          price:130,unit:'25 bags',img:I+'1627435601361-ec25f5b1d0e5?w=300&q=80'},
    {brand:'Twinings',   name:'Chamomile Tea',      price:280,unit:'20 bags',img:I+'1627435601361-ec25f5b1d0e5?w=300&q=80'},
  ]},
  { id:'coffee', name:'Coffee', cat:'Beverages', img:I+'1447933601403-0c6688de566e?w=400&q=80', types:[
    {brand:'Nescafe',    name:'Classic Instant',    price:250,unit:'100g',img:I+'1447933601403-0c6688de566e?w=300&q=80'},
    {brand:'Nescafe',    name:'Gold Blend',         price:360,unit:'100g',img:I+'1447933601403-0c6688de566e?w=300&q=80'},
    {brand:'Nescafe',    name:'Sunrise Mix',        price:180,unit:'100g',img:I+'1447933601403-0c6688de566e?w=300&q=80'},
    {brand:'Nescafe',    name:'Cold Coffee Mix',    price:150,unit:'200g',img:I+'1461023058943-07fcbe16d735?w=300&q=80'},
    {brand:'Bru',        name:'Instant Coffee',     price:220,unit:'100g',img:I+'1514432324607-a09d9b4aefdd?w=300&q=80'},
    {brand:'Bru',        name:'Gold Coffee',        price:280,unit:'100g',img:I+'1514432324607-a09d9b4aefdd?w=300&q=80'},
    {brand:'Tata',       name:'Coffee Grand',       price:230,unit:'100g',img:I+'1514432324607-a09d9b4aefdd?w=300&q=80'},
    {brand:'CCF',        name:'Filter Coffee',      price:180,unit:'200g',img:I+'1495474472287-4d71bcdd2085?w=300&q=80'},
    {brand:'Davidoff',   name:'Rich Aroma Coffee',  price:460,unit:'100g',img:I+'1447933601403-0c6688de566e?w=300&q=80'},
  ]},
  // ══ SNACKS ══
  { id:'biscuits', name:'Biscuits', cat:'Snacks', img:I+'1558961363-fa8fdf82db35?w=400&q=80', types:[
    {brand:'Parle',      name:'Parle-G',            price:10, unit:'100g',img:I+'1558961363-fa8fdf82db35?w=300&q=80'},
    {brand:'Parle',      name:'Monaco Lite',        price:15, unit:'100g',img:I+'1558961363-fa8fdf82db35?w=300&q=80'},
    {brand:'Britannia',  name:'Marie Gold',         price:30, unit:'200g',img:I+'1558961363-fa8fdf82db35?w=300&q=80'},
    {brand:'Britannia',  name:'Good Day Cashew',    price:20, unit:'100g',img:I+'1499636136210-6f4ee915583e?w=300&q=80'},
    {brand:'Britannia',  name:'Good Day Butter',    price:20, unit:'100g',img:I+'1499636136210-6f4ee915583e?w=300&q=80'},
    {brand:'Britannia',  name:'Bourbon',            price:25, unit:'150g',img:I+'1499636136210-6f4ee915583e?w=300&q=80'},
    {brand:'Britannia',  name:'50-50',              price:20, unit:'150g',img:I+'1499636136210-6f4ee915583e?w=300&q=80'},
    {brand:'Oreo',       name:'Original Cream',     price:30, unit:'120g',img:I+'1558961363-fa8fdf82db35?w=300&q=80'},
    {brand:'Oreo',       name:'Strawberry Cream',   price:30, unit:'120g',img:I+'1558961363-fa8fdf82db35?w=300&q=80'},
    {brand:'McVities',   name:'Digestive Biscuit',  price:55, unit:'250g',img:I+'1558961363-fa8fdf82db35?w=300&q=80'},
    {brand:'Sunfeast',   name:'Dark Fantasy',       price:60, unit:'100g',img:I+'1558961363-fa8fdf82db35?w=300&q=80'},
    {brand:'Sunfeast',   name:'Moms Magic',         price:25, unit:'150g',img:I+'1499636136210-6f4ee915583e?w=300&q=80'},
  ]},
  { id:'chips', name:'Chips & Namkeen', cat:'Snacks', img:I+'1566478989037-eec170784d0b?w=400&q=80', types:[
    {brand:'Lays',       name:'Classic Salted',     price:20, unit:'26g', img:I+'1566478989037-eec170784d0b?w=300&q=80'},
    {brand:'Lays',       name:'Magic Masala',       price:20, unit:'26g', img:I+'1566478989037-eec170784d0b?w=300&q=80'},
    {brand:'Lays',       name:'Spanish Tomato',     price:20, unit:'26g', img:I+'1566478989037-eec170784d0b?w=300&q=80'},
    {brand:'Kurkure',    name:'Masala Munch',       price:20, unit:'40g', img:I+'1621939514649-280e2ee25f60?w=300&q=80'},
    {brand:'Kurkure',    name:'Noodle Masala',      price:20, unit:'40g', img:I+'1621939514649-280e2ee25f60?w=300&q=80'},
    {brand:'Bingo',      name:'Mad Angles Achaari', price:20, unit:'38g', img:I+'1566478989037-eec170784d0b?w=300&q=80'},
    {brand:'Haldirams',  name:'Bhujia',             price:60, unit:'200g',img:I+'1621939514649-280e2ee25f60?w=300&q=80'},
    {brand:'Haldirams',  name:'Aloo Bhujia',        price:55, unit:'200g',img:I+'1621939514649-280e2ee25f60?w=300&q=80'},
    {brand:'Haldirams',  name:'Moong Dal Namkeen',  price:50, unit:'150g',img:I+'1621939514649-280e2ee25f60?w=300&q=80'},
    {brand:'Haldirams',  name:'Peanuts Masala',     price:30, unit:'100g',img:I+'1621939514649-280e2ee25f60?w=300&q=80'},
    {brand:'Cheetos',    name:'Crunchy Masala',     price:20, unit:'26g', img:I+'1566478989037-eec170784d0b?w=300&q=80'},
    {brand:'Act II',     name:'Butter Popcorn',     price:40, unit:'50g', img:I+'1566478989037-eec170784d0b?w=300&q=80'},
  ]},
  { id:'chocolate', name:'Chocolate', cat:'Snacks', img:I+'1549007994-cb92caebd54b?w=400&q=80', types:[
    {brand:'Cadbury',    name:'Dairy Milk',         price:40, unit:'40g', img:I+'1549007994-cb92caebd54b?w=300&q=80'},
    {brand:'Cadbury',    name:'Dairy Milk Silk',    price:62, unit:'60g', img:I+'1549007994-cb92caebd54b?w=300&q=80'},
    {brand:'Cadbury',    name:'5-Star',             price:20, unit:'22g', img:I+'1548907040-4baa42d10919?w=300&q=80'},
    {brand:'Cadbury',    name:'Perk',               price:15, unit:'20g', img:I+'1548907040-4baa42d10919?w=300&q=80'},
    {brand:'Cadbury',    name:'Munch',              price:20, unit:'26g', img:I+'1548907040-4baa42d10919?w=300&q=80'},
    {brand:'Nestle',     name:'KitKat 4 Finger',    price:30, unit:'37g', img:I+'1587132137056-bfbf0166836e?w=300&q=80'},
    {brand:'Nestle',     name:'KitKat 2 Finger',    price:15, unit:'18g', img:I+'1587132137056-bfbf0166836e?w=300&q=80'},
    {brand:'Nestle',     name:'Milkybar',           price:20, unit:'25g', img:I+'1549007994-cb92caebd54b?w=300&q=80'},
    {brand:'Mars',       name:'Snickers',           price:40, unit:'45g', img:I+'1548907040-4baa42d10919?w=300&q=80'},
    {brand:'Mars',       name:'Bounty',             price:50, unit:'57g', img:I+'1549007994-cb92caebd54b?w=300&q=80'},
    {brand:'Ferrero',    name:'Rocher 3pc Box',     price:120,unit:'37g', img:I+'1549007994-cb92caebd54b?w=300&q=80'},
    {brand:'Lindt',      name:'Dark 70%',           price:180,unit:'100g',img:I+'1606312619070-d48b4c652a52?w=300&q=80'},
  ]},
  // ══ FRUITS & VEGGIES ══
  { id:'fruits', name:'Fruits', cat:'Fruits & Veggies', img:I+'1610832958506-aa56368176cf?w=400&q=80', types:[
    {brand:'Shimla',     name:'Apple',              price:130,unit:'1kg',  img:I+'1560806887-1e4cd0b6cbd6?w=300&q=80'},
    {brand:'Imported',   name:'Fuji Apple',         price:180,unit:'1kg',  img:I+'1560806887-1e4cd0b6cbd6?w=300&q=80'},
    {brand:'Local',      name:'Banana',             price:40, unit:'dozen',img:I+'1603833665858-e61d17a86224?w=300&q=80'},
    {brand:'Ratnagiri',  name:'Alphonso Mango',     price:200,unit:'1kg',  img:I+'1605027990121-cbae9e0642df?w=300&q=80'},
    {brand:'UP',         name:'Dussehri Mango',     price:80, unit:'1kg',  img:I+'1605027990121-cbae9e0642df?w=300&q=80'},
    {brand:'Gujarat',    name:'Kesar Mango',        price:150,unit:'1kg',  img:I+'1605027990121-cbae9e0642df?w=300&q=80'},
    {brand:'Nagpur',     name:'Orange',             price:60, unit:'1kg',  img:I+'1547514701-42782101795e?w=300&q=80'},
    {brand:'Local',      name:'Mosambi',            price:55, unit:'1kg',  img:I+'1547514701-42782101795e?w=300&q=80'},
    {brand:'Local',      name:'Green Grapes',       price:70, unit:'500g', img:I+'1537640538966-79f369143f8f?w=300&q=80'},
    {brand:'Local',      name:'Black Grapes',       price:80, unit:'500g', img:I+'1537640538966-79f369143f8f?w=300&q=80'},
    {brand:'Local',      name:'Papaya',             price:45, unit:'1kg',  img:I+'1623492701902-47dc207df5bc?w=300&q=80'},
    {brand:'Local',      name:'Watermelon',         price:30, unit:'1kg',  img:I+'1563114773-84221bd62daa?w=300&q=80'},
    {brand:'Local',      name:'Pomegranate',        price:100,unit:'1kg',  img:I+'1604495772376-9657f0033fa0?w=300&q=80'},
    {brand:'Imported',   name:'Strawberry',         price:120,unit:'250g', img:I+'1464965911861-746a04b4bca6?w=300&q=80'},
    {brand:'Imported',   name:'Kiwi',               price:150,unit:'4 pc', img:I+'1585059895524-72359e06133a?w=300&q=80'},
  ]},
  { id:'veggies', name:'Vegetables', cat:'Fruits & Veggies', img:I+'1540420773420-3366772f4999?w=400&q=80', types:[
    {brand:'Local',      name:'Potato (Aloo)',      price:30, unit:'1kg',  img:I+'1508313880080-c4bef0730395?w=300&q=80'},
    {brand:'Local',      name:'Sweet Potato',       price:50, unit:'1kg',  img:I+'1508313880080-c4bef0730395?w=300&q=80'},
    {brand:'Nasik',      name:'Onion (Pyaaz)',      price:35, unit:'1kg',  img:I+'1518977822534-7049a61ee0c2?w=300&q=80'},
    {brand:'Local',      name:'Tomato',             price:40, unit:'1kg',  img:I+'1546094096-0df4bcaaa337?w=300&q=80'},
    {brand:'Local',      name:'Carrot (Gajar)',     price:40, unit:'500g', img:I+'1447175008436-054170c2e979?w=300&q=80'},
    {brand:'Local',      name:'Spinach (Palak)',    price:20, unit:'bunch',img:I+'1576045057995-568f588f82fb?w=300&q=80'},
    {brand:'Local',      name:'Methi (Fenugreek)',  price:20, unit:'bunch',img:I+'1576045057995-568f588f82fb?w=300&q=80'},
    {brand:'Local',      name:'Green Capsicum',     price:50, unit:'500g', img:I+'1563565375-f3fdfdbefa83?w=300&q=80'},
    {brand:'Local',      name:'Red Capsicum',       price:80, unit:'500g', img:I+'1563565375-f3fdfdbefa83?w=300&q=80'},
    {brand:'Local',      name:'Cauliflower (Gobi)', price:30, unit:'1 pc', img:I+'1510627498534-cf7e9002facc?w=300&q=80'},
    {brand:'Local',      name:'Brinjal (Baingan)',  price:25, unit:'500g', img:I+'1615484477778-ca3b77940c25?w=300&q=80'},
    {brand:'Local',      name:'Bhindi (Okra)',      price:35, unit:'500g', img:I+'1540420773420-3366772f4999?w=300&q=80'},
    {brand:'Local',      name:'Peas (Matar)',       price:60, unit:'500g', img:I+'1540420773420-3366772f4999?w=300&q=80'},
    {brand:'Local',      name:'Karela (Bitter Grd)',price:40, unit:'500g', img:I+'1540420773420-3366772f4999?w=300&q=80'},
    {brand:'Local',      name:'Garlic (Lehsun)',    price:50, unit:'250g', img:I+'1540420773420-3366772f4999?w=300&q=80'},
    {brand:'Local',      name:'Ginger (Adrak)',     price:40, unit:'250g', img:I+'1540420773420-3366772f4999?w=300&q=80'},
  ]},
];
 
let cartData = JSON.parse(localStorage.getItem("avinash_cart5")) || [];
let activeCategory = "All";
let expandedId = null;
 
const cats = ["All", ...new Set(catalog.map(p => p.cat))];
const catDiv = document.getElementById("categories");
cats.forEach(c => {
  const btn = document.createElement("button");
  btn.className = "cat-btn" + (c==="All"?" active":"");
  btn.textContent = c;
  btn.onclick = () => {
    activeCategory = c; expandedId = null;
    document.querySelectorAll(".cat-btn").forEach(b=>b.classList.remove("active"));
    btn.classList.add("active");
    document.getElementById("section-label").textContent = c==="All"?"All Products":c;
    renderAll();
  };
  catDiv.appendChild(btn);
});
 
function getCartQty(key){ const f=cartData.find(i=>i.key===key); return f?f.qty:0; }
function makeKey(brand,name){ return brand+'||'+name; }
 
function renderAll(){
  const search=document.getElementById("search").value.toLowerCase();
  const div=document.getElementById("products");
  div.innerHTML="";
  const filtered=catalog.filter(p=>{
    const matchCat=activeCategory==="All"||p.cat===activeCategory;
    const matchSearch=p.name.toLowerCase().includes(search)||
      p.types.some(t=>t.name.toLowerCase().includes(search)||t.brand.toLowerCase().includes(search));
    return matchCat&&matchSearch;
  });
  if(filtered.length===0){div.innerHTML='<div class="no-results">😕 No products found</div>';return;}
  const searchActive=search.length>0;
  filtered.forEach(p=>{
    const isExpanded=expandedId===p.id||searchActive;
    const matchingTypes=searchActive
      ?p.types.filter(t=>t.name.toLowerCase().includes(search)||t.brand.toLowerCase().includes(search)||p.name.toLowerCase().includes(search))
      :p.types;
    const card=document.createElement("div");
    card.className="parent-card"+(isExpanded?" expanded":"");
    card.id="parent-"+p.id;
    card.innerHTML=`
      <div class="parent-img-wrap"><img src="${p.img}" alt="${p.name}" loading="lazy"></div>
      <div class="parent-info">
        <div class="parent-name">${p.name}</div>
        <div class="parent-sub-count">${p.types.length} brands/types</div>
        <div class="expand-arrow">▼</div>
      </div>`;
    card.onclick=()=>toggleExpand(p.id);
    div.appendChild(card);
    const panel=document.createElement("div");
    panel.className="sub-panel"+(isExpanded?" open":"");
    panel.id="panel-"+p.id;
    panel.innerHTML=`
      <div class="sub-panel-title">🏷 ${p.name} — All Brands</div>
      <div class="sub-grid">
        ${matchingTypes.map(t=>{
          const key=makeKey(t.brand,t.name);
          const qty=getCartQty(key);
          const sk=key.replace(/'/g,"\\'").replace(/"/g,'&quot;');
          const dn=(t.brand+' '+t.name).replace(/'/g,"\\'");
          return `
            <div class="sub-item">
              <div class="sub-img-wrap"><img src="${t.img}" alt="${t.name}" loading="lazy" onerror="this.src='${I}1586201375761-83865001e31c?w=300&q=80'"></div>
              <div class="sub-info">
                <div class="sub-brand">${t.brand}</div>
                <div class="sub-item-name">${t.name}</div>
                <div class="sub-item-unit">${t.unit}</div>
                <div class="sub-item-price">₹${t.price}</div>
                ${qty>0?`<div class="qty-row">
                  <button onclick="event.stopPropagation();changeQty('${sk}',${t.price},-1)">−</button>
                  <span>${qty}</span>
                  <button onclick="event.stopPropagation();changeQty('${sk}',${t.price},1)">+</button>
                </div>`:''}
              </div>
              ${qty>0
                ?`<button class="add-sub-btn in-cart" onclick="event.stopPropagation();changeQty('${sk}',${t.price},1)">✓ Added</button>`
                :`<button class="add-sub-btn" onclick="event.stopPropagation();addToCart('${sk}','${dn}',${t.price})">+ Add</button>`}
            </div>`;
        }).join("")}
      </div>`;
    div.appendChild(panel);
  });
}
 
function toggleExpand(id){
  expandedId=(expandedId===id)?null:id;
  renderAll();
  if(expandedId){setTimeout(()=>{const el=document.getElementById("parent-"+id);if(el)el.scrollIntoView({behavior:'smooth',block:'start'});},100);}
}
function addToCart(key,displayName,price){
  const f=cartData.find(i=>i.key===key);
  if(f)f.qty++;else cartData.push({key,name:displayName,price,qty:1});
  saveCart();renderAll();updateFloatBtn();
  showToast("✅ "+displayName+" added!");
}
function changeQty(key,price,delta){
  const f=cartData.find(i=>i.key===key);
  if(f){f.qty+=delta;if(f.qty<=0)cartData=cartData.filter(i=>i.key!==key);}
  saveCart();renderAll();renderCartDrawer();updateFloatBtn();
}
function saveCart(){localStorage.setItem("avinash_cart5",JSON.stringify(cartData));}
function updateFloatBtn(){
  const total=cartData.reduce((s,i)=>s+i.price*i.qty,0);
  const count=cartData.reduce((s,i)=>s+i.qty,0);
  document.getElementById("cart-count").textContent=count;
  document.getElementById("float-total").textContent=total;
  document.getElementById("float-cart-btn").classList.toggle("hidden",cartData.length===0);
}
function renderCartDrawer(){
  const container=document.getElementById("cart-items");
  const footer=document.getElementById("cart-footer");
  container.innerHTML="";
  if(cartData.length===0){container.innerHTML='<div class="empty-cart"><div>🛒</div>Your cart is empty</div>';footer.innerHTML="";return;}
  let total=0;
  cartData.forEach(item=>{
    total+=item.price*item.qty;
    const d=document.createElement("div");
    d.className="cart-item";
    const sk=item.key.replace(/'/g,"\\'");
    d.innerHTML=`
      <div><div class="cart-item-name">${item.name}</div><div class="cart-item-sub">₹${item.price} each</div></div>
      <div style="display:flex;align-items:center;gap:8px;">
        <div class="cart-qty">
          <button onclick="changeQty('${sk}',${item.price},-1)">−</button>
          <span>${item.qty}</span>
          <button onclick="changeQty('${sk}',${item.price},1)">+</button>
        </div>
        <div style="font-weight:800;min-width:55px;text-align:right;">₹${item.price*item.qty}</div>
        <button class="remove-btn" onclick="removeItem('${sk}')">🗑</button>
      </div>`;
    container.appendChild(d);
  });
  footer.innerHTML=`
    <div class="total-row"><span>Total (${cartData.reduce((s,i)=>s+i.qty,0)} items)</span><span>₹${total}</span></div>
    <div class="btn-row">
      <button class="clear-btn" onclick="clearCart()">🗑 Clear</button>
      <button class="order-btn" onclick="orderWhatsApp()">📲 Order on WhatsApp</button>
    </div>`;
}
function removeItem(key){cartData=cartData.filter(i=>i.key!==key);saveCart();renderAll();renderCartDrawer();updateFloatBtn();}
function clearCart(){if(!confirm("Clear all items?"))return;cartData=[];saveCart();renderAll();renderCartDrawer();updateFloatBtn();showToast("🗑 Cart cleared");}
function openCart(){renderCartDrawer();document.getElementById("cart-overlay").classList.add("open");document.getElementById("cart-drawer").classList.add("open");}
function closeCart(){document.getElementById("cart-overlay").classList.remove("open");document.getElementById("cart-drawer").classList.remove("open");}
function showToast(msg){const t=document.getElementById("toast");t.textContent=msg;t.classList.add("show");setTimeout(()=>t.classList.remove("show"),2000);}
function orderWhatsApp(){
  if(cartData.length===0){
    alert("Cart is empty!");
    return;
  }

  // Address input popup
  let address = prompt("📍 Enter your delivery address:");

  if(!address || address.trim()===""){
    alert("Address is required!");
    return;
  }

  let msg = "Hello Avinash Store%0A";
  msg += "📦 Order Details:%0A";

  let total = 0;

  cartData.forEach(item=>{
    msg += `${item.name} x${item.qty} - Rs.${item.price*item.qty}%0A`;
    
    total += item.price*item.qty;
  });

  msg += `%0A💰 Your Total Amount: Rs.${total}%0A`;
  msg += `📍 Address: ${encodeURIComponent(address)}`;

  window.open(`https://wa.me/917011869015?text=${msg}`);
}
renderAll();updateFloatBtn();
</script>
</body>
</html>
