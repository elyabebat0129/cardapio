<script setup>
import { ref, computed, onMounted } from 'vue'
import MenuForm from './components/MenuForm.vue'
import MenuFilters from './components/MenuFilters.vue'
import MenuItem from './components/MenuItem.vue'

// Estado principal
const itens = ref([])
const filtroAtual = ref('Todas')

// Métodos
const adicionarItem = (novoItem) => {
  itens.value.push({ ...novoItem, id: Date.now() })
}
const removerItem = (id) => {
  itens.value = itens.value.filter(item => item.id !== id)
}
</script>

<template>

</template>