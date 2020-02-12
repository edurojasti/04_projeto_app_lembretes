<template>
    <div class="lembrete mb-4">
        <div class="row">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-body">
                        <h5 class="text-dark">Registrar</h5>
                        <div class="input-group">
                            <input type="text" class="form-control" placeholder="Insira o lembrete" v-model="lembrar" v-on:keyup.enter="addLembrete(lembrar)">
                            <div class="input-group-append">
                            <button 
                            class="btn btn-warning" 
                            type="button" 
                            v-on:click="addLembrete(lembrar)">
                                <span class="fa fa-plus"></span>
                            </button>
                            </div>
                        </div>
                        <hr>
                        <h5 class="text-dark">
                            Lembretes
                            <span class="badge badge-warning">{{lembretes.length}}</span>
                            </h5>
                        <ul class="list-group">
                            <li class="list-group-item" v-for="lembrar in lembretes" v-bind:key="lembrar">
                                <div class="row">
                                    <div class="col-8">
                                        <p class="mt-2" style="font-size: 19px">{{lembrar}}</p>
                                    </div>
                                    <div class="col-4 text-center">
                                        <button class="btn btn-dark mt-2 botoees">
                                            <span class="fa fa-trash"></span>
                                        </button>
                                        <br>
                                        <span style="font-size: 14px">Excluir</span>
                                    </div>
                                </div>
                            </li>
                        </ul>
                        <clearStorage></clearStorage>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css"
import "font-awesome/css/font-awesome.css"
import jquery from 'jquery'
import clearStorage from "./clearStorage"
let $ = jquery

export default {
    name: 'lembrete',
    components: {
        clearStorage,
    },
    data: ()=>{
        return {
            lembrar: "",
            lembretes : [],
        }
    },

    methods:{
        addLembrete(lembrete){    
            if(this.lembrar == ""){
                alert("Insira uma tarefa válida!")
            }else{
                //inserindo ao localStorage
                let valorCHAVE = localStorage.getItem('keyID')
                if(valorCHAVE == undefined || valorCHAVE == ""){
                    valorCHAVE = 1
                    localStorage.setItem('keyID', valorCHAVE)
                }else{
                    valorCHAVE = parseInt(valorCHAVE)
                    valorCHAVE++
                    localStorage.setItem('keyID', valorCHAVE)
                }
                let NovoLembrete = {
                    id: valorCHAVE,
                    desc: lembrete
                }
                let salvarLembrete = JSON.stringify(NovoLembrete)
                localStorage.setItem(valorCHAVE, salvarLembrete)
                // alert('Item registrado com sucesso!')
                this.lembrar = ""
                location.reload();         
            }
        },
    },
    
    created(){
        $(document).ready(()=>{
            //recuperando Lembretes
            let pegarDados = localStorage.getItem('keyID')
            pegarDados = parseInt(pegarDados)

            for(let x = 1; x <= pegarDados; x++){
                let item = localStorage.getItem(x)
                item = JSON.parse(item)
                console.log(item)
                if(item === null){
                    continue
                }
                this.lembretes.push(item.desc)
            }
            console.log(this.lembretes)

            for(let i = 0; i < this.lembretes.length; i++){
                setTimeout(() => {
                    let botoes = document.querySelectorAll(".botoees")
                    console.log(botoes)
                    botoes[i].id
                }, 700);
            }


            // setTimeout(() => {
            //     let btns = document.querySelectorAll(".botoees")
            //     for(let x = 0; x <= pegarDados; x++){
            //         let item = localStorage.getItem(x)
            //         item = JSON.parse(item)
            //         console.log(item)
            //         if(item === null){
            //             continue
            //         }
            //         btns[x-1].id = item.id
            //         btns[x-1].onclick = (()=>{
            //             // alert(btns[x-1].id)
            //             localStorage.removeItem(item.id)
            //             location.reload()
            //         })
            //     }
            //     console.log(btns)
            // }, 1200)
        })
    }
  
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Titillium+Web&display=swap');
body{
  background: #f3f3f3;
  font-family: 'Titillium Web', sans-serif;
}

.lembrete{
  border-radius: 5px;
  border: 4px solid gray;
  padding: 15px;
  box-shadow: 5px 10px;
  width: 420px;
  margin: auto auto;
}

hr{
    width: 330px;
}

@media (max-width: 420px){
    .lembrete, hr{
        width: auto;
    }
}

</style>
