<template>
    <div class="foodItem">
        <div class="image-area">
            <img :src="food.image" :alt="food.name">
        </div>
        <div class="title-area">
            <span>{{food.name}}</span><span class="price">${{food.price}}</span>
        </div>
        <div class="text-area">
            <p>{{food.text}}</p>
        </div>
        <div class="order-button">
            <button @click="AddItemtoCart()">Add to Cart</button>
        </div>
    </div>
</template>
<script>
export default {
    props: ['food'],
    methods: {
        AddItemtoCart(){
            this.$emit('addfood')
        }
    },
}
</script>
<style>
    
    .foodItem{
        background: white;
        padding: 1rem 0;
    }
    .title-area{
        display: flex;
        justify-content: space-between;
        margin: .5rem;
        padding: 0 1.5rem;
        font-size: 20px;
        letter-spacing: 1px;
        font-weight: 700;
    }
    .price{
        padding: 2px 3px;
        background: #474787;
        color: white;
    }
    .text-area p{
        font-size: 14px;
        letter-spacing: 1px;
        padding: 0 1rem;
        margin-top: 1rem;
    }
    .order-button button{
        margin-top: 1.5rem;
        background: #474787;
        color: #fff;
        padding: .5rem 1rem;
        cursor: pointer;
        transition: .5s;
        border: none;
        border-radius: 5px;
        font-size: 18px;
    }
    .order-button button:hover{
        background: #000;
    }

    @media screen and (max-width: 768px) {
        .foodItem{
            padding: .5rem 0;
            margin: 1rem 0;
        }
        img{
            height: 200px;
            width: 300px;
            padding: 0;
            margin: 0;
        }
    }
</style>