<template>

    <div class="container-fluid container-lg my-5 px-sm-5 px-md-3">
        <form @submit="modal($event)" action="">
            <div class="row">
                <div class="col-12 col-md-6">
                    <label for="" class="form-label">Nome*</label>
                    <input type="text" class="form-control" v-model="nome" placeholder="Digite seu nome" aria-label="" maxlength="50" minlength="3" required>
                </div>
                <div class="col-12 col-md-6">
                    <label for="" class="form-label">CEP*</label>
                    <input type="text" v-mask="'#####-###'" @focusout="apiCep" v-model="cepValue" id="cep" class="form-control" placeholder="00000-000" aria-label="" required>
                </div>
            </div>

            <div class="row mt-3">
                <div class="col-12 col-md-6">
                    <label for="" class="form-label">Email*</label>
                    <input type="email" class="form-control" v-model="email" placeholder="Digite seu e-mail" aria-label="" required>
                </div>
                <div class="col-12 col-md-4">
                    <label for="" class="form-label">Endereço*</label>
                    <input type="text" v-model="endereco" class="form-control" placeholder="Digite seu endereço" aria-label="" maxlength="30" minlength="3" required>
                </div>
                <div class="col-12 col-md-2">
                    <label for="" class="form-label">Número*</label>
                    <input type="text" class="form-control" v-model="numero" placeholder="" aria-label="" maxlength="10" minlength="1" required>
                </div>
            </div>

            <div class="row mt-3">
                <div class="col-12 col-md-6">
                    <label for="" class="form-label">CPF*</label>
                    <input type="text" v-mask="'###.###.###-##'" v-model="cpf" id="cpf" class="form-control" placeholder="000.000.000-00" aria-label="" required>
                </div>
                <div class="col-12 col-md-3">
                    <label for="" class="form-label">Complemento*</label>
                    <input type="text" class="form-control" v-model="complemento" placeholder="" aria-label="" maxlength="20" minlength="3" required>
                </div>
                <div class="col-12 col-md-3">
                    <label for="" class="form-label">Bairro*</label>
                    <input type="text" v-model="bairro" class="form-control" placeholder="" aria-label="" maxlength="30" minlength="3" required>
                </div>
            </div>

            <div class="row mt-3">
                <div class="col-12 col-md-3">
                    <label for="" class="form-label">Data nascimento*</label>
                    <input type="text" v-mask="'##/##/##'" v-model="dataNascimento" class="form-control" placeholder="dia/mês/ano" aria-label="" required>
                </div>
                <div class="col-12 col-md-3">
                    <label for="" class="form-label">Telefone*</label>
                    <input type="text" v-mask="'(##) #####-####'" v-model="telefone" class="form-control" placeholder="(00) 00000-0000" aria-label="" required>
                </div>
                <div class="col-12 col-md-4">
                    <label for="" class="form-label">Cidade*</label>
                    <input type="text" v-model="cidade" class="form-control" placeholder="" aria-label="" maxlength="20" minlength="2" required>
                </div>
                <div class="col-12 col-md-2">
                    <label for="" class="form-label">Estado*</label>
                    <select class="form-select" aria-label="Default select example" required>
                        <option selected>{{estado}}</option>
                        <option value="">AC</option>
                        <option value="">AL</option>
                        <option value="">AP</option>
                        <option value="">AM</option>
                        <option value="">BA</option>
                        <option value="">CE</option>
                        <option value="">DF</option>
                        <option value="">ES</option>
                        <option value="">GO</option>
                        <option value="">MA</option>
                        <option value="">MT</option>
                        <option value="">MS</option>
                        <option value="">MG</option>
                        <option value="">PR</option>
                        <option value="">PB</option>
                        <option value="">PA</option>
                        <option value="">PE</option>
                        <option value="">PI</option>
                        <option value="">RN</option>
                        <option value="">RS</option>
                        <option value="">RJ</option>
                        <option value="">RO</option>
                        <option value="">RR</option>
                        <option value="">SC</option>
                        <option value="">SE</option>
                        <option value="">SP</option>
                        <option value="">TO</option>                   
                    </select>
                </div>
            </div>

            <div class="my-5 text-end">
                <button class="btn py-2 px-4" data-bs-toggle="modal" data-bs-target="#exampleModal" >Concluir compra</button>
            </div>
        </form>
    </div>

</template>
<script>
    export default{
        name:'FormCompra',

        data(){
            return{
                nome:'',
                cepValue:'',
                email:'',
                endereco:'',
                complemento:'',
                bairro:'',
                cidade:'',
                estado:'Selecione...',
                numero:'',
                cpf:'',
                dataNascimento:'',
                telefone:''
            }
        },

        methods: {
            //api ViaCep
            async apiCep(){          
                const url = `http://viacep.com.br/ws/${this.cepValue}/json/`;                
                const dados = await fetch(url);
                const endereco = await dados.json();
                //preenchimento dos campos do formulário
                this.endereco = endereco.logradouro
                this.bairro = endereco.bairro
                this.cidade = endereco.localidade   
                this.estado =endereco.uf              
            },
            //SweetAlert, biblioteca de alertas
            modal(e){
                e.preventDefault()
                Swal.fire({
                    icon: 'success',
                    title: '',
                    text: 'Seucadastrado foi solicitado com sucesso!',
                    showConfirmButton: false,
                    footer: '<a style="color: #8E37BB; text-decoration: none" class="fw-bold" href="/"><i class="fas fa-long-arrow-alt-left"></i> VOLTAR PARA HOME</a>'
                    })
            },

            
           
        }
    }

</script>

<style src="./style.scss" lang="scss" scoped />