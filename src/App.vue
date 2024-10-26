<script setup>
import { reactive } from 'vue';

const nome = "Ramon Freire"
const meuObjeto = {
  nome: "Ramon",
  filmeFavorito: "Interstelar"
}

function dizOla(nome) {
  return `${nome} diz oi`;
}

const enderecoDaImagemDoFilme = "https://t.ctcdn.com.br/KFtpt7j7YHGvJLw2o336J8axQvs=/640x360/smart/i445725.png"

const imagemDark = "https://fly.metroimg.com/upload/q_85,w_700/https://uploads.metroimg.com/wp-content/uploads/2020/04/14111110/dark-netflix1.jpg"



const gostaDoInterestelar = true
const gostaDoDark = false

const estaAutorizado = false

const botaoEstaDesabilitado = true

// let contador = 0

const estado = reactive ({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['ramon', 'gian', 'eliza', 'monica', 'luisa'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function alteraEvento (evento) {
  estado.email = evento.target.value
}

function mostraSaldoFuturo() {
  const {saldo, transferindo} = estado;
  return saldo - transferindo;
}

function validaValorTransferecia(){
  const {saldo, transferindo} = estado;
  return saldo >= transferindo
}


function cadastraNome() {
  if (estado.nomeAInserir.length >= 3) {
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("digite mais caracteres")
  } 
} 


</script>



<template>
 <h1>{{ dizOla("VueJS") }}</h1>
 <img v-if="gostaDoInterestelar":src="enderecoDaImagemDoFilme" alt="">
<img v-else-if="gostaDoDark" :src="imagemDark" alt="">
<h2 v-else>Não curte nenhum dos dois filmes</h2>

<h1 v-if="estaAutorizado">Bem-vindo</h1>
<h1 v-else>não possui acesso</h1>

<button :disabled="botaoEstaDesabilitado">Enviar mensagem</button>

<br>
<hr>

{{ estado.contador }}

<button @click="incrementar" type="button">+</button>
<button @click="decrementar" type="button">-</button>

<br>
<hr>

{{ estado.email }}
<input type="email" @keyup="alteraEvento">

<br>
<hr>

Saldo: {{ estado.saldo }} <br>
Transferindo: {{ estado.transferindo }} <br>
Saldo Depois da Transferencia: {{ mostraSaldoFuturo() }} <br>
<input :class="{ invalido: !validaValorTransferecia()}" @keyup="evento=>estado.transferindo = evento.target.value" type="number" placeholder="Quantia a transferir">
<button v-if="validaValorTransferecia()">Transferir</button>
<span v-else>Valor maior que o saldo</span>

<br>
<hr>

<ul>
  <li v-for="nome in estado.nomes">
    {{ nome }}
  </li>
</ul>
<input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
<button @click="cadastraNome" type="button">Cadastrar nome</button>

<h3 v-for="nome in estado.nomes">{{ nome }}</h3>

</template>

<style scoped>
img {
  max-width: 200px;
}

.invalido { 
  outline-color: red;
  border-color: red;
}

</style>
