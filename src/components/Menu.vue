
<template>
  <button @click="showFood()">{{item}}</button>
</template>

<script>
export default {
    props: ['item'],
    methods: {
      showFood(){
        this.$emit('showFood')
      }
    },
}
</script>

<style scoped>
    button{
        color: #000;
        background: #fff;
        padding: .5rem 1rem;
        margin: 1rem;
        align-content: center;
        text-transform: capitalize;
        font-size: 18px;
        font-weight: 700;
        border-radius: 5px;
        cursor: pointer;
        border: none;
        transition: .5s;
    }
    button:hover{
        background: #000;
        color: #fff;
        
    }


@media screen and (max-width: 768px) {
  button{
    font-size: 14px;
    border-radius: 3px;
    margin: 1rem .5rem;
    padding: .5rem 0rem;
  }
}
</style>