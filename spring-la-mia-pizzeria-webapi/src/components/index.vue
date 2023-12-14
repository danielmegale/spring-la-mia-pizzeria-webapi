<script>
import axios from 'axios';

export default {
    data() {
        return {
            pizzas: [],
            originalPizzas: [],
            searchQuery: '',
        };
    },
    mounted() {
        this.fetchPizzas();
    },
    methods: {
        fetchPizzas() {
            const apiUrl = 'http://localhost:8080/api/v1.0/pizzas';
            axios.get(apiUrl)
                .then(response => {
                    this.pizzas = response.data;
                    this.originalPizzas = response.data;
                    console.log('Dati ricevuti:', this.pizzas);
                })
                .catch(error => {
                    console.error('Errore durante la chiamata:', error);
                });
        },
        searchPizza() {
            if (this.searchQuery.trim() === '') {
                this.pizzas = this.originalPizzas;
                return;
            }

            const filteredPizzas = this.originalPizzas.filter(pizza => {
                return pizza.nome.toLowerCase().includes(this.searchQuery.toLowerCase());
            });

            this.pizzas = filteredPizzas;

            console.log('Dati della ricerca:', this.pizzas);
        },

        deletePizza(pizzaId) {
            const apiUrl = `http://localhost:8080/api/v1.0/pizzas/${pizzaId}`;
            axios.delete(apiUrl)
                .then(response => {
                    console.log('Pizza eliminata con successo:', response.data);
                    this.fetchPizzas();
                })
                .catch(error => {
                    console.error('Errore durante l\'eliminazione della pizza:', error);
                });
        },
    }
}
</script>

<template>
    <h1>Pizze</h1>
    <form @submit.prevent="searchPizza" method="get">
        <input v-model="searchQuery" @input="searchPizza" type="text" placeholder="Cerca una pizza">
    </form>
    <ul>
        <li v-for="pizza in pizzas" :key="pizza.id">
            {{ pizza.nome }} {{ pizza.prezzo }}€
            <button @click="deletePizza(pizza.id)">Elimina</button>
            <br>
            {{ pizza.descrizione }}
        </li>
    </ul>
</template>

<style></style>
