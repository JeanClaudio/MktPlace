<template>

    <div class="container-fluid container-xl my-5">
        <div class="row borderTable py-2 d-none d-md-flex">
            <div class="col-3">
                <h3>PRODUTOS</h3>
            </div>
            <div class="col-3">
                <h3>QUANTIDADE</h3>
            </div>
            <div class="col-3">
                <h3>VALOR UNITÁRIO</h3>
            </div>
            <div class="col-3">
                <h3>TOTAL</h3>
            </div>            
        </div>

        <!------------------------>
        
            <div v-for="(produto,index) in carrinho" v-bind:key="index" class="row borderTable py-2">
                <div class="col-12 col-md-3 ">
                   <div class="row text-center">
                    <i @click="removeCarrinho(index)" class="fas fa-trash-alt my-auto fs-4 col-2 d-none d-md-block"></i>
                    <div class="col-12 col-md-10">
                        <h3 class="d-block d-md-none text-center mob_style fs-1">PRODUTO</h3>
                        <p class="categ">{{carrinho[index].category}}</p>
                        <p class="itemcart fs-5">{{carrinho[index].name}}</p>
                    </div>
                   </div>
                </div>

                <div class="col-12 col-md-3 d-flex justify-content-center align-items-center">
                    <div class="row container">
                        <h3 class="d-block d-md-none text-center mob_style">Quantidade</h3>
                            <div class="input-group mb-3 d-flex justify-content-center justify-content-md-start px-0">
                                <span @click="subtraiNoTotal(carrinho[index].price, index), subtraiItem(index), atPrecoMais(index, index+'preco', carrinho[index].price, index+'precoParcelado')" class="input-group-text border btn fw-bold hovereffect">-</span>
                                    <div :id="index" class="value border d-flex justify-content-center align-items-center">{{1}}</div>
                                <span @click="addItem(index), atPrecoMais(index, index+'preco',carrinho[index].price, index+'precoParcelado'), somaNoTotal(carrinho[index].price)" class="input-group-text border btn fw-bold hovereffect">+</span>
                            </div>

                            <div class="col-6 m-auto text-center d-block d-md-none">
                                <h3 class="d-block d-md-none text-center mob_style">Valor unit.</h3>
                                <p><span class="fw-bold">R$ {{carrinho[index].price}}</span> à vista<br>ou 10x {{(carrinho[index].price /10).toFixed(2)}}</p>  
                            </div>
                            <div class="col-6 m-auto text-center d-block d-md-none">
                                <h3 class="d-block d-md-none text-center mob_style">Valor total</h3>
                                <p>R$ 
                                    <span :id="index+'preco'" class="fw-bold">{{carrinho[index].price}}</span> 
                                    à vista<br>
                                    ou 10x <span :id="index+'precoParcelado'">{{(carrinho[index].price /10).toFixed(2)}}</span>
                                </p>   
                            </div>
                            <div class="col-12 text-center d-md-none px-5 my-3">   
                                <button @click="removeCarrinho(index)" class="btn btn-danger" type="button"> Excluir item<i  class="fas fa-trash-alt ms-3 d-md-none"></i></button>
                            </div>
                    </div>
                </div>

                <div class="col-12 col-md-3 d-flex align-items-center d-none d-md-block">
                    <p><span class="fw-bold">R$ {{carrinho[index].price}}</span> à vista<br>ou 10x {{(carrinho[index].price /10).toFixed(2)}}</p>  
                </div>
                <div class="col-12 col-md-3 d-flex align-items-center d-none d-md-block">
                    <p>
                        <span :id="index+'preco'" class="fw-bold">R$ {{carrinho[index].price}}</span> 
                        à vista<br>
                        ou 10x R$ <span :id="index+'precoParcelado'">{{(carrinho[index].price /10).toFixed(2)}}</span>
                    </p>                                  
                </div>
                       
            </div>
        <!------------------------>       

       

        <div id="totalCompra" class="text-center text-md-end py-3 py-md-5 ">            
            <p class="fw-bold fs-4">TOTAL A VISTA    <br class="d-md-none">            
                <span id="somaTotal" class="categ fs-3 ms-md-5">R$ {{(totalCompra).toFixed(2)}}</span>
            </p>
            <p> <span class="me-md-4 fw-bold fs-4">TOTAL PARCELADO <br class="d-md-none"></span> em até 10x <span class="fw-bold">R$ {{(totalCompra /10).toFixed(2)}}</span><br>(total R$  {{(totalCompra).toFixed(2)}} )</p>  
            
            <div class="col-12 text-center d-md-none px-5 my-5 ">   
                <button class="btn btn-danger mx-4 " type="button"> Limpar carrinho<i  class="fas fa-trash-alt ms-3 d-md-none"></i></button>
            </div>
        </div>

        <div class="row py-4">
            <div class="col-8 fw-bold d-flex justify-content-center justify-content-md-start d-none d-md-flex">
                <i @click="limparCarrinho" class="fas fa-trash-alt my-auto fs-4 me-3"></i><p class="my-auto">Limpar carrinho</p>                
            </div>
            
            <div class="col-12 col-md-4 d-flex justify-content-center justify-content-md-end ">
                <a href="/"><button class="btn btnContComprando py-2 px-4 fw-bold">Continuar comprando</button></a>
            <a href="/formulario"><button class="btn btnConcluirCompra ms-4 py-2 px-4 fw-bold">Concluir compra</button></a>
            </div>
        </div>
    </div>
    
  
</template>
  
  <script>
      export default{
          name: 'CarTabela',

          data(){
            return{
                carrinho:[],
                totalCompra:''
            }
          },

          mounted(){           
            const prodCarrinho =JSON.parse(localStorage.getItem('produtosCarrinho'))
            this.carrinho = prodCarrinho
            
            //Atualiza total a pagar ao carregar a tela
            for (let i = 0; i < this.carrinho.length; i++) {                
                this.totalCompra = parseInt( this.totalCompra +  this.carrinho[i].price)
            }

          },

          methods:{
            
            removeCarrinho(index){
                alert("item apagado")
                //remove produto na tela           
                this.carrinho.splice(index,1)
                //recupera itens do localStorage para atualizar
                const prodCarrinho =JSON.parse(localStorage.getItem('produtosCarrinho'))
                //atualiza localStorage retirando o item excluido
                prodCarrinho.splice(index,1)
                //envia para o localStorage com os itens já atualizados
                localStorage.setItem('produtosCarrinho',JSON.stringify(prodCarrinho))

                //Atualiza icone com do carrinho
                document.getElementById('cartItens').innerHTML = prodCarrinho.length

                //Faz a soma do valor total dos itens ao carregar a página
                this.totalCompra = 0
                for (let i = 0; i < this.carrinho.length; i++) {                     
                    this.totalCompra = parseInt( this.totalCompra +  this.carrinho[i].price)
                 }                
            },

            subtraiItem(index){   
                //Remove item do carrinho             
                var qtd = document.getElementById(index).innerHTML                
                if(qtd > 1){
                    qtd = parseInt(qtd) -1                
                document.getElementById(index).innerHTML = qtd
                }              
            },

            addItem(index){
                //Adiciona item no carrinho
                var qtd = document.getElementById(index).innerHTML                
                qtd = parseInt(qtd) +1
                document.getElementById(index).innerHTML = qtd
            },

            atPrecoMais(idOne, idTwo, preco, idThree, idFour){
                //Atualiza preço quando número de produtos aumenta ou diminiu                
                var multiplicador = document.getElementById(idOne).innerHTML //pega o valor da quantidade de itens                   
                var novopreco = document.getElementById(idTwo) //pega o id da tag que vai receber o novo preço                  
                novopreco.innerHTML = (preco * multiplicador).toFixed(2) //Atualiza o preço
                document.getElementById(idThree).innerHTML = (novopreco.innerHTML /10).toFixed(2)//Atualiza preço parcelado
            },

            somaNoTotal(preco){            
                //Atualiza total a pagar quando um item é adicionado
                this.totalCompra = this.totalCompra + preco
            },

            subtraiNoTotal(preco, id){
                //Atualiza total a pagar quando um item é removido 
                var condi = document.getElementById(id).innerHTML
                if(condi > 1){
                    this.totalCompra = this.totalCompra - preco
                }
            },

            limparCarrinho(){
                this.carrinho = []
                this.totalCompra = 0                
                localStorage.removeItem("produtosCarrinho");
                alert("Carrinho apagado com sucesso!")
            }
            
          }
      }
  </script>
  
  <style src="./style.scss" lang="scss" scoped />