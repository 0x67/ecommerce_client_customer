<template>
  <div id="home">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarTogglerDemo01" aria-controls="navbarTogglerDemo01" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarTogglerDemo01">
        <a class="navbar-brand" href="#">BliBli</a>
        <ul class="navbar-nav mr-auto mt-2 mt-lg-0">
          <li class="nav-item active">
            <p></p>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <router-link to="/carts">
            <button class="btn btn-info btn-lg" style="margin-right: 10px;">
              <svg width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-cart-check-fill" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M.5 1a.5.5 0 0 0 0 1h1.11l.401 1.607 1.498 7.985A.5.5 0 0 0 4 12h1a2 2 0 1 0 0 4 2 2 0 0 0 0-4h7a2 2 0 1 0 0 4 2 2 0 0 0 0-4h1a.5.5 0 0 0 .491-.408l1.5-8A.5.5 0 0 0 14.5 3H2.89l-.405-1.621A.5.5 0 0 0 2 1H.5zM4 14a1 1 0 1 1 2 0 1 1 0 0 1-2 0zm7 0a1 1 0 1 1 2 0 1 1 0 0 1-2 0zm.354-7.646a.5.5 0 0 0-.708-.708L8 8.293 6.854 7.146a.5.5 0 1 0-.708.708l1.5 1.5a.5.5 0 0 0 .708 0l3-3z"/>
              </svg>
              Your Cart
            </button>
          </router-link>
          <router-link to="/login">
            <button @click="logout" class="btn btn-info btn-lg">
            <span class="glyphicon glyphicon-log-out"></span> Log out
            </button>
          </router-link>
        </form>
      </div>
    </nav>

    <div class="product-container">
      <div class="card-group">
        <div class="card product" style="width: 18rem;" v-for="(product, id) in products" :key="id">
        <a style="align-text: center;" target="_blank" :href="product.image_url">
          <img class="card-img-top" :src="product.image_url" alt="https://www.kenangan.com/assets/img/no_image.jpg">
        </a>
        <div class="card-body">
          <h5 class="card-title"><strong>{{ product.category }}</strong></h5>
          <p class="card-text">{{ product.name}}</p>
          <div class="d-flex justify-content-between">
              <p class="card-text"><small>{{ product.price }}</small></p>
              <p class="card-text"><small v-if="product.stock == 0">Out of Stock</small></p>
              <p class="card-text"><small v-if="product.stock > 0">{{ product.stock }}</small></p>
            </div>
            <button @click="addToCart(product.id)" class="btn btn-primary">
              <svg width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-cart-plus-fill" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M.5 1a.5.5 0 0 0 0 1h1.11l.401 1.607 1.498 7.985A.5.5 0 0 0 4 12h1a2 2 0 1 0 0 4 2 2 0 0 0 0-4h7a2 2 0 1 0 0 4 2 2 0 0 0 0-4h1a.5.5 0 0 0 .491-.408l1.5-8A.5.5 0 0 0 14.5 3H2.89l-.405-1.621A.5.5 0 0 0 2 1H.5zM4 14a1 1 0 1 1 2 0 1 1 0 0 1-2 0zm7 0a1 1 0 1 1 2 0 1 1 0 0 1-2 0zM9 5.5a.5.5 0 0 0-1 0V7H6.5a.5.5 0 0 0 0 1H8v1.5a.5.5 0 0 0 1 0V8h1.5a.5.5 0 0 0 0-1H9V5.5z"/>
              </svg> Add To Cart
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  methods: {
    fetchAllProducts () {
      this.$store.dispatch('fetchAllProducts')
    },
    addToCart (id) {
      const payload = {
        ProductId: id,
        quantity: 1
      }
      this.$store.dispatch('addToCart', payload)
        .then(() => {
          this.$router.push({ name: 'Cart' })
        })
    },
    logout () {
      this.$store.dispatch('logout')
    }
  },
  created () {
    this.fetchAllProducts()
  },
  computed: {
    products () {
      return this.$store.state.products
    }
  }
}

</script>

<style scoped>
  nav {
    background-color: #739299;
    margin-bottom: 75px;
  }

  .product-container {
    display: flex;
    justify-content: center;
  }

  .product {
    margin: 20px;
  }

  img {
    display: flex;
    border: 1px solid #ddd;
    border-radius: 4px;
    max-width: 100%;
    height: auto;
  }

  img:hover {
    box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
  }

  .card-img-top {
    min-height: 120px;
    max-height: auto;
    float: left;
    padding: 3px;
  }
</style>
