<template>
    <div class="corpo">
        <h1 class="centralizado">{{msg}}</h1>
        <!-- <h1>{{msg}}</h1>
        <h2>{{titulo}}</h2>
        <h3 v-text="titulo + ' olá'"></h3> -->
        <!-- propriedade v-model alem de ler, altera a origem atraves do input -->
        <!-- <input v-model="message"> -->
        <!-- podemos trocar a diretiva v-on: utilizando apenas o @
        <button v-on:click="reverseMessage">Inverter</button>
        <p>{{message}}</p>
        <p v-text="titulo + new Date().toLocaleString()"></p> -->
        
        <!-- <span v-if="seen">Mostra Isso</span>
        <img :src="foto.url" :alt="foto.alt"> -->
        <input v-on:input="filtro = $event.target.value" type="search" placeholder="filtre pelo nome da foto" class="filtro"/>
        <ul class="lista-fotos">
            <li v-for="user in fotosComFiltro" :key="user.id" class="lista-fotos-item"> 
                <meu-painel :titulo="user.first_name + ' ' + user.last_name">
                    <img
                        class="imagem-responsiva"
                        :src="user.avatar"
                        :alt="user.first_name + user.last_name"
                        :title="user.first_name + user.last_name"
                    />
                </meu-painel>
            </li>
        </ul>
    </div>

</template>

<script>
import axios from "axios";
import Painel from "./shared/Painel"
export default {
    computed: {
        fotosComFiltro(){
            if(this.filtro){
                let exp = new RegExp(this.filtro.trim(), "i");
                return this.users.filter(user => exp.test(user.first_name))
            }else {
                return this.users
            }
        }
    },
    components: {
        //alias para tag
        "meu-painel": Painel
    },
    name: "Tela",
    created() {
        axios
            .get("https://reqres.in/api/users")
            // promisse
            .then(response =>{
                this.users = response.data.data
            })
            .catch(e => {
                this.erros.push(e)
            })
    },
    props: {
        msg: String
    }, 
    methods: {
        reverseMessage(){
            this.message = this.message.split('').reverse().join('')
        }
    },
    data(){
        return {
            message: "Texto a ser invertido: romano acata amores a damas amadas e Roma ataca o namoro",
            titulo : "Titulo da minha página",
            seen: false,
            foto: {
                url: "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTwV4kVzT5McBdGSgqlVeRzubrNH_mOrrkKseDOGFURq20HmsrelEfMU7It",
                alt: "Cachorro"
            },
            fotos: [
                {
                    id: 0,
                    url: "https://images.pexels.com/photos/2220336/pexels-photo-2220336.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260",
                    alt: "Leão"
                },
                {
                    id: 1,
                    url: "https://images.pexels.com/photos/34700/bear-animals-zoo-captivity.jpg?auto=compress&cs=tinysrgb&h=750&w=1260",
                    alt: "Urso"
                },
                {
                    id: 2,
                    url: "https://images.pexels.com/photos/35992/gorilla-monkey-ape-zoo.jpg?auto=compress&cs=tinysrgb&h=750&w=1260",
                    alt: "Gorilla"
                }
                
            ],
            users: [],
            erros: [],
            filtro: ""
        }
    },
}
</script>

<style scoped>

.filtro {
    display: block;
    width: 100%;
    height: 44px;
    padding: 5px;
    font-size: 16px;
}

.centralizado {
  text-align: center;
}

.corpo {
  font-family: Helvetica, Arial, sans-serif;
  margin: 0 auto;
  width: 96%;
  color: gray;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}

/* estilo do painel */

.imagem-responsiva {
    width: 100%;
  }

</style>
