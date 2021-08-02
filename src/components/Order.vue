<template>
  <div class="order">
      <div class="status">
          <p>Your food is being prepared. We will notify you once its ready.</p>
      </div>
      <div class="close-button">
          <button @click="closeOrderView()">X</button>
      </div>
      <div class="order-id">
          Order: {{order.orderID}}
      </div>
  <div class="order-details" v-for="(item,index) in order.orderItems" :key="index">
      <div class="each-item">
          <p>{{item.name}} - ${{item.price}} x {{item.quantity}}</p>
      </div>
  </div>
  <div class="total-bill">
      <p>Total Bill: ${{order.orderBill}}</p>
  </div>
  </div>
</template>

<script>
export default {
    props: ['order'],
    methods: {
        closeOrderView(){
            this.$emit('closeOrderView')
        }
    },
}
</script>

<style scoped>
    
    *{
        color: #000;
    }
    .order{
        position: fixed;
        top: 5%;
        left: 50%;
        transform: translateX(-50%);
        background: #fff;
        padding: 1rem 5rem;
        border: 3px solid #000;
        border-radius: 5px;
        transition: .5s;
    }
    .status{
        background: rgb(90, 187, 147);
        padding: .5rem;
        margin-bottom: 1rem;
    }
    .order-id{
        margin-bottom: 1rem;
        font-size: 25px;
        font-weight: 700;
        color: #000;
    }

    .each-item p{
        font-size: 20px;
        margin: 1rem 0;
        padding: .5rem 0;
        background: #474787;
        color: #fff;
    }

    .total-bill p{
        font-size: 25px;
        font-weight: 700;
    }
    .close-button{
        position: absolute;
        right: 1%;
        top: 2%;
    }
    .close-button button{
        border: none;
        background: #000;
        color: #fff;
        border-radius: 2px;
        font-weight: 700;
        padding: .2rem .5rem;
        cursor: pointer;
    }

    @media screen and (max-width: 768px) {

    .order{
        top: 8%;
        width: 250px;
        padding: 1rem 2rem;

    }
    .order-id,.total-bill p{
        font-size: 18px;
    }

    .each-item p{
        font-size: 15px;
    }
}
</style>