<template>
    <div>
        <hr>
        <button class="btn btn-danger btn-block mt-2" v-on:click="apagarTudo()">
            Remover Todos <span class="fa fa-trash"></span>
        </button>
    </div>   
</template>

<script>
import jquery from 'jquery'
let $ = jquery
import "bootstrap/dist/css/bootstrap.css"
import "popper.js"
import "bootstrap/dist/js/bootstrap.js"
import "font-awesome/css/font-awesome.css"


export default {
    name: 'clearStorage',
    methods: {
        apagarTudo(){
            localStorage.clear()
            alert('Lembretes deletados com sucesso!')
            location.reload()
        }
    },

    created(){
        $('#meuModal').on('shown.bs.modal', function () {
            $('#meuInput').trigger('focus')
        })
    }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Titillium+Web&display=swap');
</style>
