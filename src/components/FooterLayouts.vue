<template>
  <footer class="footer">
    <div class="footer__content content-item">
      <div class="content-item-left">
        <ul>
          <li><a href="">Пунукт 01</a></li>
          <li><a href="">Пунукт 02</a></li>
          <li><a href="">Пунукт 03</a></li>
          <li><a href="">Пунукт 04</a></li>
          <li><a href="">Пунукт 05</a></li>
          <li><a href="">Пунукт 06</a></li>
          <li><a href="">Пунукт 07</a></li>

        </ul>
        <ul>
          <li><a href="">Пунукт 08</a></li>
          <li><a href="">Пунукт 09</a></li>
          <li><a href="">Пунукт 10</a></li>
          <li><a href="">Пунукт 11</a></li>
          <li><a href="">Пунукт 12</a></li>
          <li><a href="">Пунукт 13</a></li>
          <li><a href="">Пунукт 14</a></li>

        </ul>
      </div>
      <div class="content-item-center">
        <ul>
          <li><a href="">Поисковое продвижение сайтов</a></li>
          <li><a href="">Тариф "Новый"</a></li>
          <li><a href="">Тариф "Новый"</a></li>
          <li><a href="">Тариф "Новый"</a></li>
          <li><a href="">Тариф "Новый"</a></li>
          <li><a href="">Тариф "Новый"</a></li>
          <li><a href="">Тариф "Новый"</a></li>
        </ul>
      </div>
      <div class="content-item-right">
        <div class="content-item-right-top"></div>
        <div class="content-item-right-bottom"></div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {

}
</script>

<style scoped>
.content-item {
    display: flex;
    margin:20px auto 20px auto;
    border-top: 2px solid black;
    padding-top: 20px;
    flex-wrap: wrap;
    gap: 20px;
}
.footer__content{
}

@media(max-width:938px){
    .content-item div {
        width: 70%;

    }
    .content-item-right-top,.content-item-right-bottom{
        width: 100%!important;
    }
    .content-item{
        justify-content: center;
    }
}
@media(max-width:500px){
    .content-item{
        width: 400px;
    }
}

.content-item-left {
    background-color: #777777;
    width: 300px;
    height: 180px;
    display: flex;
    flex-wrap: wrap;
}

.content-item-left ul li {
    list-style: none;
}

.content-item-left ul li a {
    color: white;
    text-decoration: none;
}

.content-item-center {
    background-color: #777777;
    width: 300px;
    height: 180px;
    flex-wrap: wrap;
}

.content-item-center ul li{
    text-align: left;
}
.content-item-center ul li a{
    color:white;
    text-decoration: none;
}

.content-item-right {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 300px;
    height: 180px;
    flex-wrap: wrap;
}

.content-item-right-top {
    background-color: #777777;
    width: 307px;
    height: 80px;
}

.content-item-right-bottom {
    background-color: #777777;
    width: 307px;
    height: 73px;
}
</style>