<template>
  <div class="home">
      <Notice :order="placedOrder" v-if="placedOrder" @show="showOrder"/>
      <Order v-if="isShowOrder" :order="placedOrder" @closeOrderView="closeViewOrder()"/>
      <div class="cart">
        <div class="cart-title">
          <p v-if="totalOrder === 0">Empty Stack</p>
          <p v-if="totalOrder > 0">Your Stack - {{totalOrder}}</p>
        </div>
        <div class="order-items" v-if="totalOrder > 0">
           <div class="horizontal-line"></div>
          <div class="cart-items" v-if="totalOrder > 0">
            <Cart v-for="(item, index) in cart" :key="index" :food="item" @add="addToCart(item)" @remove="removeFromCart(item)"/>
          </div>
          <div class="horizontal-line"></div>
          <div class="total-bill">
            <p>Total Bill: ${{totalBill}}</p>
          </div>
          <div class="cehckout-button">
            <button @click="checkOut">Place Order</button>
          </div>
        </div>
      </div>
      <div class="menu">
        <h3>Menu</h3>
        <div class="menu-icon" @click="toggleMobileMenu()">
          <p></p>
          <p></p>
          <p></p>
        </div>
        <div class="menus" v-bind:class="{active: isActive}">
          <Menu v-for="(item,index) in categories" :key="index" :item="item" @showFood="filterFoods(item)"/>
        </div>
      </div>
      <div class="container">
        <div class="all-foods">
        <Food v-for="(item, index) in filteredFoods" :key="index" :food="item" @addfood="addToCart(item)"/>
      </div>
      </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Notice from '../components/Notice.vue'
import Cart from '../components/Cart.vue'
import Menu from '../components/Menu.vue'
import Food from '../components/Food.vue'
import Order from '../components/Order.vue'

export default {
  name: 'Home',
  components: {
    Notice,
    Cart,
    Menu,
    Food,
    Order,
  },
  methods: {

    // Filtering all available foods based on the category
    filterFoods(category){
      if(category === 'all'){
        this.filteredFoods = this.foods
        console.log(category,this.filteredFoods);
      }
      else{
        this.filteredFoods = this.foods.filter(food => food.category === category)
      }
    },

    /// Add to cart handler for each food
    addToCart(item){
      this.totalOrder++
      if(this.cart.length === 0){
        item.quantity = 1
        this.cart.push(item)
        console.log("First Item pushed");
      }else{
        if(!this.cart.includes(item)){
          item.quantity = 1
          this.cart.push(item)
          console.log("New Item pushed");
        }else{
          this.cart.map(food => {
            if(food.id === item.id){
              food.quantity ++
              console.log(`${item.name} quantity updated`);
            }
          })
        }
      }
      let totalprice = 0;
      this.cart.map(food => {
        // const price = food.price * food.quantity
        totalprice += food.price * food.quantity
      })
      this.totalBill = totalprice
    },
    removeFromCart(item){
      this.cart.map(food => {
        if(food.id === item.id && food.quantity > 0){
          this.totalOrder--
          food.quantity --
        }
      })
      let totalprice = 0;
      this.cart.map(food => {
        // const price = food.price * food.quantity
        totalprice -= food.price * food.quantity
      })
      this.totalBill = totalprice
    },
    toggleMobileMenu(){
      this.isActive = !this.isActive
    },
    checkOut(){
      const order = {
        orderItems: this.cart,
        orderBill: this.totalBill,
        orderID: new Date().getTime().toString()
      }
      this.placedOrder = order
      this.cart = []
      this.totalOrder = 0
      console.log(this.placedOrder);
    },
    showOrder(){
      this.isShowOrder = true
    },

    // Close order view pop up window
    closeViewOrder(){
      this.isShowOrder = false
    }
  },
  data() {
    return {
      categories: [],
      filteredFoods: [],
      totalOrder: 0,
      cart: [],
      totalBill: null,
      isActive:false,
      placedOrder:'',
      isShowOrder: false,
      foods: [
        {
          id:1,
          category: 'breakfast',
          image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/RedDot_Burger.jpg/1200px-RedDot_Burger.jpg',
          name: 'Hamburger',
          price: 10,
          text: 'A hamburger is a food, typically considered a sandwich, consisting of one or more cooked patties of ground meat, usually beef, placed inside a sliced bread roll or bun',
        },
        {
          id:2,
          category: 'breakfast',
          image: 'https://upload.wikimedia.org/wikipedia/commons/f/ff/Egg_Sandwich.jpg',
          name: 'Sandwich',
          price: 5,
          text: 'A sandwich is a food typically consisting of vegetables, sliced cheese or meat, placed on or between slices of bread wherein bread serves as a container for another food type.',
        },
        {
          id:3,
          category: 'lunch',
          image: 'https://media-cdn.tripadvisor.com/media/photo-s/11/09/77/07/500g-tomahawk-steak-done.jpg',
          name: 'T-bone Steak',
          price: 30,
          text: 'The T-bone and porterhouse are steaks of beef cut from the short loin. Both steaks include a "T"-shaped lumbar vertebra with sections of abdominal internal oblique muscle on each side.',
        },
        {
          id:4,
          category: 'lunch',
          image: 'https://www.bakespace.com/images/large/f468b5f5247496b4f854e203bd46a7cd.jpeg',
          name: 'Biryani',
          price: 15,
          text: 'Biryani is a mixed rice dish originating among the Muslims of the Indian subcontinent. It is made with Indian spices, rice, and meat usually that of chicken, goat, lamb, prawn, fish, and sometimes, in addition, eggs or vegetables such as potatoes in certain regional varieties.',
        },
        {
          id:5,
          category: 'dinner',
          image: 'https://s3-ap-southeast-1.amazonaws.com/media.evaly.com.bd/media/images/7c047620d38f-bbq-pizza.jpg',
          name: 'Pizza',
          price: 12,
          text: 'Pizza is an Italian dish consisting of a usually round, flattened base of leavened wheat-based dough topped with tomatoes, cheese, and often various other ingredients, which is then baked at a high temperature, traditionally in a wood-fired oven. A small pizza is sometimes called a pizzetta.',
        },
        {
          id:6,
          category: 'dinner',
          image: 'https://therecipecritic.com/wp-content/uploads/2019/07/easy_fried_rice-1-500x500.jpg',
          name: 'Fried Rice',
          price: 10,
          text: 'Fried rice is a dish of cooked rice that has been stir-fried in a wok or a frying pan and is usually mixed with other ingredients such as eggs, vegetables, seafood, or meat.',
        },
        {
          id:7,
          category: 'shakes',
          image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/68/Strawberry_milk_shake_%28cropped%29.jpg/220px-Strawberry_milk_shake_%28cropped%29.jpg',
          name: 'Milkshake',
          price: 5,
          text: 'A milkshake is a sweet drink made by blending milk, ice cream, and flavorings or sweeteners such as butterscotch, caramel sauce, chocolate syrup, fruit syrup, or whole fruit into a thick, sweet, cold mixture.',
        },
      ]
    }
  },
  mounted() {
      const allCategories = [];
      this.foods.map(food => {
        allCategories.push(food.category)
      })
      this.categories = ['all',...new Set(allCategories)]
    },
  created() {
    this.filteredFoods = this.foods
  },
}
</script>


<style scoped>

  .container{
    max-width: 60vw;
  }
  .cart{
    border: 3px solid #fff;
    position: fixed;
    top: 2%;
    right: 2%;
    padding: 1rem;
    background: #474787;
  }
  .cart-title p{
    color: #fff;
    font-weight: 700;
    font-size: 20px;
  }

  .horizontal-line{
    height: 1px;
    background: #fff;
    margin: .5rem;
  }

  .total-bill{
    color: #fff;
  }

  .menu h3{
    color: #fff;
    font-size: 30px;
    font-weight: 700;
  }

  .menu-icon{
    position: fixed;
    display: none;
    margin-left: 3px;
  }

  .active button{
    display: block;
  }

  .menu-icon p{
    height: 2px;
    width: 2rem;
    background: #fff;
    margin: .5rem 0;
  }

  .all-foods{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 3rem;
  }

  .cehckout-button button{
        margin-top: 1.5rem;
        background: #fff;
        color: #000;
        padding: .5rem 1rem;
        cursor: pointer;
        transition: .5s;
        border: none;
        border-radius: 5px;
        font-size: 18px;
  }
  .cehckout-button button:hover{
    background: #000;
    color: #fff;
  }
  @media screen and (max-width: 768px) {
    .container{
      max-width: 80vw;
    }
    .menu-icon{
      display: block;
    }
    .menus{
      display: none;
    }
    .active{
      display: block;
      position: fixed;
      left: 8%;
      width: 50%;
      background: #474787;
      transition: .5s;
    }
    .menu button{
      padding: .5rem;
      margin: .5rem auto;
      width: 95%;
      transition: .5s;
    }
    .all-foods{
      display: block;
    }
    .cart{
      border: 1px solid #fff;
      position: fixed;
      top: 1%;
      right: 1%;
      padding: .5rem;
      background: #474787;
    }

  .cart-title p{
    color: #fff;
    font-weight: 500;
    font-size: 16px;
  }

    .cehckout-button button{
        margin-top: 1rem;
        padding: .5rem .5rem;
        border-radius: 3px;
        font-size: 15px;
  }
    
  }

</style>
