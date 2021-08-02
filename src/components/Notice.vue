<template>
  <div class="notice">
      <p>Your order #<span class="order-link" @click="showOrder">{{order.orderID}}</span> has been placed successfully</p>
  </div>
  <router-view/>
</template>

<script>
export default {
  props: ['order'],
  methods: {
    showOrder(){
      this.$emit('show')
    }
  },
}
</script>

<style>
    .notice{
        position: absolute;
        top: 2%;
        left: 50%;
        transform: translateX(-50%);
        color: white;
        font-size: 20px;
        font-weight: 700;
    }
    .order-link{
      text-decoration: underline;
      font-weight: 700;
      color: #fff;
      cursor: pointer;
    }
@media screen and (max-width: 768px) {
  .notice{
    font-size: 10px;
    top: 2%;
    left: 5%;
    transform: translateX(-20%);
    margin-left: 2.5rem;
  }
  .notice p{
    font-weight: 500;
  }
}
</style>