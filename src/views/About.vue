<template>
  <div class="about">
    <div class="container">
      <div class="image">
        <img :src="companyInfo.image" :alt="companyInfo.name">
      </div>
      <div class="title">
        <h1>{{companyInfo.name}}</h1>
      </div>
      <div class="info">
        <p>{{companyInfo.about}}</p>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      companyInfo: {
        name: 'KFC',
        about: "KFC is an American fast food restaurant chain headquartered in Louisville, Kentucky that specializes in fried chicken. It is the world's second-largest restaurant chain after McDonald's, with 22,621 locations globally in 150 countries as of December 2019. The chain is a subsidiary of Yum! ",
        image: 'https://media.apnarm.net.au/media/images/2020/02/21/v3imagesbina3b4d1b383c51568860f55cd442a00e0-smpqf9rm5lpzzeadvt2_t1880.jpg',
      },
    }
  },
}
</script>


<style scoped>
.container{
  margin-top: 2rem;
}
  img{
    width: 45vw;
    border: 5px solid #fff;
    border-radius: 5px;
  }
  .title{
    color: #fff;
    margin: 2rem 0;
    font-size: 30px;
    letter-spacing: 5px;
  }
  .info{
    max-width: 40vw;
    margin: 0 auto;
    align-items: center;
  }
  .info p{
    text-align: left;
    color: #fff;
    letter-spacing: 2px;
    font-size: 18px;
  }

  @media screen and (max-width: 768px) {
  
  img{
    width: 100%;
  }
  .title{
    margin: 1rem 0;
    font-size: 20px;
  }
  .info{
    max-width: 100%;
  }
  .info p{
    letter-spacing: 1px;
    font-size: 15px;
    margin-left: .5rem;
  }
  }
</style>