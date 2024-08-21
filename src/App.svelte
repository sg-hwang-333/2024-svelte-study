<script>
  let cart = [];

  function addToCart(productId) {
    cart = [...cart, productId];
  }

  let product= {
    id: 'svelte-book',
    name: 'Svelte Guide',
    price: 30000,
    images: [
      "https://github.com/developer-book/svelte/raw/main/static/svelte-book-1.png",
      "https://github.com/developer-book/svelte/raw/main/static/svelte-book-2.png",
      "https://github.com/developer-book/svelte/raw/main/static/svelte-book-3.png"
    ]
  }

  let relatedProducts = [
    {
      id: "react-book",
      name: 'React Book',
      price: 30000
    },
    {
      id: "vue-book",
      name: 'Vue Book',
      price: 30000
    },
    {
      id: "angular-book",
      name: 'Angular Book',
      price: 30000
    }
  ]

  // 이미지 슬라이더를 위한 변수&함수 
  let sliderCenterIndex = 0;
  let sliderLeftIndex = product.images.length -1;
  let sliderRightIndex = 1;

  function sliderMoveLeft() {
    const length = product.images.length;
    sliderCenterIndex = (sliderCenterIndex - 1 + length) % length;
    sliderLeftIndex = (sliderCenterIndex - 1 + length) % length;
    sliderRightIndex = (sliderCenterIndex + 1) % length;
  }

  function sliderMoveRight() {
    const length = product.images.length;
    sliderCenterIndex = (sliderCenterIndex + 1) % length;
    sliderLeftIndex = (sliderCenterIndex - 1 + length) % length;
    sliderRightIndex = (sliderCenterIndex + 1) % length;
  }
</script>

<header class="header">
  <a class="header-title" href="/">Svelte Site</a>
  <nav>
    <ul class="header-links">
      <li>안녕하세요, 게스트님</li>
      <li>
        <a href="/cart">장바구니(0)</a>
      </li>
    </ul>
  </nav>
</header>

<article class="product">
  <div class="product-main">
    <div class="image-container">
       <div class="slider">
        <img src="{product.images[sliderLeftIndex]}" class="slider-item left" alt="">
        <img src="{product.images[sliderCenterIndex]}" class="slider-item" alt="">
        <img src="{product.images[sliderRightIndex]}" class="slider-item right" alt="">
        <button class="slider-left-button" on:click={sliderMoveLeft}>◀</button>
        <button class="slider-right-button" on:click={sliderMoveRight}>▶</button>
       </div>
    </div>

    <div>
      <h2>{product.name}</h2>
      <dl>
        <dt>금액</dt>
        <dd>{product.price}원</dd>
      </dl>
      <div>
        { #if !cart.includes(product.id) }
          <button on:click={() => addToCart(product.id)}>장바구니 담기</button>
        { :else }
          <button disabled>장바구니 담기 완료</button> 
        { /if } 
      </div>
    </div>
  </div>

  <footer>
    <h3>관련상품</h3>
    <ul>
      {#each relatedProducts as product}
        <li><a href="/products/{[product.id]}">{product.name}</a> - {product.price}원</li>
      {/each}
    </ul>
  </footer>
</article>

<style>
  :global(body) {
    margin: 0 0;
    padding: 0 0;
    background-color: #eee;
  }
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 auto;
    background-color: #fff;
    padding: 0 15px;
    width: 100%;
    max-width: 800px;
    height: 50px;
  }
  .header-title {
    font-weight: bold;
  }
  .header-links {
    display: flex;
    gap: 10px;
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .product {
    margin: 0 auto;
    background-color: #fff;
    padding: 15px;
    width: 100%;
    max-width: 800px;
 }
 .product-main {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
 }
 .image-container {
  width: 100%;
  max-width: 400px;
  overflow: hidden;
 }
 .image-container img {
  width: 100%;
 }
 footer > *{
  list-style: none;
 }

 /* slider */
 .slider {
  position: relative;
  width: 80%;
  margin: 0 10%;
 }
 .slider-item {
  width: 100%;
 }
 .slider-item.left {
  position: absolute;
  top: 0;
  right: 100%;
 }
 .slider-item.right {
  position: absolute;
  top: 0;
  left: 100%;
 }
 .slider-left-button {
  position: absolute;
  top: 50%;
  right: 100%;
 }
 .slider-right-button {
  position: absolute;
  top: 50%;
  left: 100%;
 }
</style>