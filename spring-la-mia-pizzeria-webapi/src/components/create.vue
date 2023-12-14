<script>
import axios from 'axios';

export default {
    data() {
        return {
            showComponent: false,
            pizza: {
                nome: '',
                descrizione: '',
                // Altri campi della pizza, se necessario
            },
        };
    },
    methods: {
        addPizza() {
            const apiUrl = 'http://localhost:8080/api/v1.0/pizzas';

            axios.post(apiUrl, this.pizza)
                .then(response => {
                    console.log('Pizza aggiunta con successo:', response.data);
                    window.location.reload();
                })
                .catch(error => {
                    console.error('Errore durante l\'aggiunta della pizza:', error);
                });
        },
    },
};
</script>

<template>
    <div>
        <!-- <button v-if="!showComponent" @click="showComponent = true">
            Aggiungi Una Pizza
        </button> -->
        <!-- <div v-if="showComponent"> -->
        <h1>Aggiungi una nuova pizza</h1>
        <form @submit.prevent="addPizza">
            <div>
                <label for="pizzaNome">Nome: </label>
                <input v-model="pizza.nome" type="text" id="pizzaNome" required>
            </div>
            <div>
                <label for="pizzaDescrizione">Descrizione: </label>
                <input type="text" v-model="pizza.descrizione" id="pizzaDescrizione" required>
            </div>
            <div>
                <label for="pizzaPrezzo">Prezzo: </label>
                <input type="text" v-model="pizza.prezzo" id="pizzaPrezzo" required>
            </div>

            <!-- Altri campi della pizza, se necessario -->

            <button type="submit">Aggiungi Pizza</button>
        </form>
        <!-- </div> -->
    </div>
</template>

<style></style>
