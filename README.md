# Andypor
<html><head><base href="https://websim.ai/restaurant-order/">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>美食點餐平台</title>
<style>
  body {
    font-family: 'Microsoft JhengHei', Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f5f5f5;
  }
  .header {
    background-color: #ff7043;
    color: white;
    text-align: center;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
  }
  .menu {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
  }
  .menu-item {
    background-color: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    transition: transform 0.3s ease;
  }
  .menu-item:hover {
    transform: translateY(-5px);
  }
  .menu-item img {
    width: 100%;
    height: 150px;
    object-fit: cover;
  }
  .menu-item-info {
    padding: 1rem;
  }
  .menu-item-title {
    font-size: 1.2rem;
    font-weight: bold;
    margin-bottom: 0.5rem;
  }
  .menu-item-price {
    color: #ff7043;
    font-weight: bold;
  }
  .add-to-cart {
    background-color: #ff7043;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  .add-to-cart:hover {
    background-color: #f4511e;
  }
  .cart {
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    background-color: #ff7043;
    color: white;
    padding: 1rem;
    border-radius: 50%;
    box-shadow: 0 2px 4px rgba(0,0,0,0.2);
    cursor: pointer;
  }
  .cart-count {
    position: absolute;
    top: -5px;
    right: -5px;
    background-color: white;
    color: #ff7043;
    border-radius: 50%;
    padding: 0.25rem 0.5rem;
    font-size: 0.8rem;
    font-weight: bold;
  }
  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
    40% {transform: translateY(-10px);}
    60% {transform: translateY(-5px);}
  }
</style>
</head>
<body>
  <div class="header">
    <h1>美食點餐平台</h1>
  </div>
  <div class="container">
    <div class="menu" id="menu"></div>
  </div>
  <div class="cart" id="cart">
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
      <circle cx="9" cy="21" r="1"></circle>
      <circle cx="20" cy="21" r="1"></circle>
      <path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"></path>
    </svg>
    <span class="cart-count" id="cartCount">0</span>
  </div>

  <script>
    const menuItems = [
      { id: 1, name: '紅燒牛肉麵', price: 120, image: 'beef-noodle.jpg' },
      { id: 2, name: '滷肉飯', price: 60, image: 'braised-pork-rice.jpg' },
      { id: 3, name: '蚵仔煎', price: 80, image: 'oyster-omelette.jpg' },
      { id: 4, name: '珍珠奶茶', price: 50, image: 'bubble-tea.jpg' },
      { id: 5, name: '小籠包', price: 100, image: 'xiaolongbao.jpg' },
      { id: 6, name: '鹽酥雞', price: 70, image: 'fried-chicken.jpg' },
    ];

    const menuContainer = document.getElementById('menu');
    const cartCount = document.getElementById('cartCount');
    let cart = [];

    function renderMenu() {
      menuItems.forEach(item => {
        const menuItem = document.createElement('div');
        menuItem.className = 'menu-item';
        menuItem.innerHTML = `
          <img alt="${item.name}，台灣傳統美食照片" src="${item.image}" width="200" height="150">
          <div class="menu-item-info">
            <div class="menu-item-title">${item.name}</div>
            <div class="menu-item-price">NT$ ${item.price}</div>
            <button class="add-to-cart" data-id="${item.id}">加入購物車</button>
          </div>
        `;
        menuContainer.appendChild(menuItem);
      });
    }

    function addToCart(id) {
      const item = menuItems.find(item => item.id === id);
      cart.push(item);
      updateCartCount();
      animateCart();
    }

    function updateCartCount() {
      cartCount.textContent = cart.length;
    }

    function animateCart() {
      const cartElement = document.getElementById('cart');
      cartElement.style.animation = 'bounce 0.5s';
      setTimeout(() => {
        cartElement.style.animation = '';
      }, 500);
    }

    renderMenu();

    document.addEventListener('click', (e) => {
      if (e.target.classList.contains('add-to-cart')) {
        const id = parseInt(e.target.getAttribute('data-id'));
        addToCart(id);
      }
    });

    document.getElementById('cart').addEventListener('click', () => {
      alert(`購物車內容：\n${cart.map(item => `${item.name} - NT$ ${item.price}`).join('\n')}\n總計：NT$ ${cart.reduce((sum, item) => sum + item.price, 0)}`);
    });
  </script>
</body></html>

