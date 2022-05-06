<template>
  <header class="header">
    <div class="header-logo"></div>
    <div class="header-contact">
    </div>
    <div class="header-more">
      <ul>
        <li><a href="tel:+375(29)3711041">+375 (29) 371-10-41</a></li>
        <li><a href=""><u>info@increase.by</u></a></li>
        <li><a href=""><u>www.increase.by</u></a></li>
      </ul>
    </div>
  </header>
</template>

<script>
export default {
  return: {}
}


</script>

<style scoped>
.header {
    margin: 20px auto 20px auto;
    display: flex;
    border-bottom: 2px solid black;
    align-items: center;
    flex-wrap: wrap;
    gap: 20px;
    padding-bottom: 20px;
}

@media (max-width: 954px) {
    .header-more {
        width: 50rem !important;
        display: flex;
        justify-content: flex-end;
    }
}

@media (max-width: 788px) {
    .header-more {
        width: 100px;

    }

    .header div {

    }

    .header-logo {
        width: 100px !important;
    }
}

@media (max-width: 636px) {
    .header {
        flex-direction: column;
        width: 100%;
    }


    .header div {
        width: 500px;
    }

    .header-more {
        width: 500px!important;
        text-align: center !important;
        align-items: center;
        justify-content: flex-end;
    }

    .header-logo {
        width: 500px !important;
        text-align: center !important;
        align-items: center;
        justify-content: flex-end;
    }

}
@media (max-width: 500px) {
    .header div {
        width: 300px;
    }
    .header-more {
        width: 300px!important;
        text-align: center !important;
        align-items: center;
        justify-content: center;
    }

    .header-logo {
        width: 300px !important;
        text-align: center !important;
        align-items: center;
        justify-content: center;
    }

}
.header div {
    height: 108px;
    background-color: #777777;
}


li {
    text-decoration: none;
    list-style: none;
    margin-bottom: 5px;
    text-align: end;
}

.header-logo {
    width: 121px;
}

.header-contact {
    align-items: center;
    width: 280px;
    background-color: #777777;

}

.header-more {
    text-align: right;
    width: 535px;
    background-color: #777777;
}

@media (max-width: 636px) {
    .header-more {
        text-align: center;
    }
}

.header-contact ul li {
    list-style: none;
    align-items: center;
    text-align: center;
}

.header-contact ul li a {
    text-decoration: none;
    color: white;
}

.header-contact ul {
    display: flex;
    justify-content: space-around;
}


.header-more ul li a {
    text-decoration: none;
    color: white
}
</style>