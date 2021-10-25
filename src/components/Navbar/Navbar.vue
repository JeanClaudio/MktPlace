<template>

  <nav class="navbar navbar-light bg-light ">   
    <div id="cont" class="container-fluid container-xl py-3 px-lg-5">
        <a class="navbar-brand mx-1 mx-sm-5" href="/"><h1>Mkt<span>Place</span></h1></a>

        
            <div class="d-flex justify-content-center align-items-center">
              <a class="navbar-brand" href="/carrinho">
              <p class="my-auto fw-bold d-none d-sm-block fs-5">Produtos</p>
            </a>
              <a class="navbar-brand" href="/carrinho">
                <i id="cart" class="fas fa-shopping-cart mx-1 mx-sm-5 position-relative ">
                  <span id="cartItens" class="position-absolute top-100 start-100 translate-middle badge rounded-pill bg-danger">
                    {{numItenCar}}
                    <span class="visually-hidden">unread messages</span>
                  </span>
                </i>
              </a> 

            </div>
            
            
    </div>
  </nav>

  

</template>

<script>
    export default{
        name: 'Navbar',

        data(){
          return{
            numItenCar:'0'
          }
        },

        mounted(){
          const prodCarrinho =JSON.parse(localStorage.getItem('produtosCarrinho'))
          this.numItenCar = prodCarrinho.length
        }
    }
</script>

<style src="./style.scss" lang="scss" scoped />
