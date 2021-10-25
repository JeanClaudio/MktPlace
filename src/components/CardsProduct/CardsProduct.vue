<template>

    <div class="containe-fluid container-xl px-2">
        <div class="row">

        <!--------------Card---------------> 
        <div v-for="(produto,index) in productApi" v-bind:key="index" class="px-2 pb-5 col-12 col-sm-6 col-md-4">
            <div class=" p-0 shadow cardes">
                <img id="Imgbanner2" class="img-fluid" :src="productApi[index].imageUrl" alt="">
                <div class="p-3 p-xl-4">
                    <p class="categoria">{{productApi[index].category}}</p>
                    <h3 id="prodName" class="fs-5 fw-bold">{{productApi[index].name}}</h3>
                    <p id="descricao" >{{productApi[index].description}}...</p>
                    <h4 class="fw-bold py-1">R$ {{productApi[index].price}}</h4>
                </div>
                <button :id="productApi[index].id" @click="addCarrinho(productApi[index])" class="py-3">Adicionar ao carrinho</button>
            </div>
        </div>    
        <!--------------Card Fim--------------->

        </div>
    </div>
    
  
</template>
  
  <script>
      export default{
        name: 'Footer',

        data(){
            return{
                productApi:[],
                prodCarrrinho:[]
            }
        },

        async mounted(){ 
                //Busca os produtos da api e adiciona esses produtos no array "productApi"
                const url = `https://raw.githubusercontent.com/owInteractive/desafio-frontend-2020/master/produtos.json`;                
                const dados = await fetch(url);
                const produtos = await dados.json();            
                this.productApi = produtos                  
        }, 

        methods:{
            addCarrinho(id){    
           
                 //Vai buscar dados no localStorage e se não encontrar cria um array vazio para receber itens adicionados no carrinho 
                const localStCarrinho = JSON.parse(localStorage.getItem('produtosCarrinho'))
                if(localStCarrinho == null){
                    localStorage.setItem('produtosCarrinho','[]')
                }else{
                    this.prodCarrrinho = localStCarrinho
                }

                //adiciona o no array "prodCarrrinho" as informações do produto e depois manda para o localStorage
                this.prodCarrrinho.push(id)
                localStorage.setItem('produtosCarrinho',JSON.stringify(this.prodCarrrinho))
                alert("Produto adicionado ao carrinho")

                //Atualiza icone do navbar com quantidade de itens no carrinho
                document.getElementById('cartItens').innerHTML = this.prodCarrrinho.length 
            }
        }
    }
  </script>
  
  <style src="./style.scss" lang="scss" scoped />