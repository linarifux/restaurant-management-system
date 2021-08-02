<template>
  <div class="each-item" v-if="food.quantity > 0">
    <button @click="removeItem">-</button>
    <p>{{food.name}} - ${{food.price}} x {{food.quantity}}</p>
    <button @click="addItem">+</button>
  </div>
</template>

<script>
export default {
    props: ['food'],
    methods: {
        addItem(){
            this.$emit('add')
        },
        removeItem(){
            this.$emit('remove')
        }
    },
}
</script>

<style scoped>

    button{
        margin: .5rem .5rem;
        padding: .5rem 1rem;
        border: none;
        border-radius: 2px;
        align-items: center;
        cursor: pointer;
    }
    button:hover{
        background: #000;
        color: #fff;
    }
    p{
        font-weight: 700;
        font-size: 16px;
    }
    .each-item{
        display: flex;
        align-items: center;
        color: white;
        justify-content: space-between;
    }

    @media screen and (max-width: 768px) {
        button{
            padding: .2rem .5rem;
        }
        p{
            font-weight: 500;
            font-size: 12px;
        }
    }

</style>