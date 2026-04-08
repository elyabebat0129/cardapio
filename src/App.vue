<script setup>
import { computed, onMounted, ref } from 'vue'
import MenuFilters from './components/MenuFilters.vue'
import MenuForm from './components/MenuForm.vue'
import MenuItens from './components/MenuItens.vue'

const itens = ref([])
const filtroAtual = ref('Todas')

const categorias = ['Todas', 'Lanche', 'Bebida', 'Sobremesa']

const itensFiltrados = computed(() => {
  if (filtroAtual.value === 'Todas') {
    return itens.value
  }

  return itens.value.filter((item) => item.categoria === filtroAtual.value)
})

const totalDisponiveis = computed(() => {
  return itens.value.filter((item) => item.disponivel).length
})

const precoMedioVisivel = computed(() => {
  if (itensFiltrados.value.length === 0) {
    return 0
  }

  const soma = itensFiltrados.value.reduce((acumulador, item) => {
    return acumulador + item.preco
  }, 0)

  return soma / itensFiltrados.value.length
})

const adicionarItem = (novoItem) => {
  itens.value.push({
    id: Date.now(),
    ...novoItem,
  })
}

const alterarFiltro = (categoria) => {
  filtroAtual.value = categoria
}

const removerItem = (id) => {
  itens.value = itens.value.filter((item) => item.id !== id)
}

onMounted(() => {
  itens.value = [
    {
      id: 1,
      nome: 'X-Burguer',
      preco: 22,
      categoria: 'Lanche',
      disponivel: true,
    },
    {
      id: 2,
      nome: 'Refrigerante',
      preco: 8,
      categoria: 'Bebida',
      disponivel: false,
    },
    {
      id: 3,
      nome: 'Petit Gateau',
      preco: 18,
      categoria: 'Sobremesa',
      disponivel: true,
    },
  ]
})
</script>

<template>
  <main class="container">
    <header class="hero">
      <h1>Cardapio Digital</h1>
    </header>

    <section class="bloco resumo">
      <div class="resumo-card">
        <span>Total de itens</span>
        <strong>{{ itens.length }}</strong>
      </div>

      <div class="resumo-card">
        <span>Disponiveis</span>
        <strong>{{ totalDisponiveis }}</strong>
      </div>

      <div class="resumo-card">
        <span>Preco medio visivel</span>
        <strong>R$ {{ precoMedioVisivel.toFixed(2) }}</strong>
      </div>
    </section>

    <div class="layout">
      <div>
        <MenuForm @add-item="adicionarItem" />
      </div>

      <div class="painel-direito">
        <MenuFilters
          :categorias="categorias"
          :filtro-atual="filtroAtual"
          @change-filter="alterarFiltro"
        />

        <MenuItens :itens="itensFiltrados" @remove-item="removerItem" />
      </div>
    </div>
  </main>
</template>

<style scoped>
:global(body) {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(180deg, #fff8f1 0%, #ffe8d9 100%);
  color: #3b1d18;
}

:global(*) {
  box-sizing: border-box;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 32px 20px 48px;
}

.hero {
  margin-bottom: 24px;
}

.tag {
  margin: 0 0 8px;
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #b45309;
}

h1 {
  margin: 0 0 10px;
  font-size: clamp(2rem, 4vw, 3.3rem);
}

.descricao {
  max-width: 620px;
  margin: 0;
  line-height: 1.5;
  color: #6b3e35;
}

.bloco {
  margin-bottom: 24px;
}

.resumo {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}

.resumo-card {
  padding: 18px;
  border-radius: 16px;
  background: #fffdfb;
  border: 1px solid #f3d4bf;
  box-shadow: 0 10px 24px rgba(88, 45, 32, 0.08);
}

.resumo-card span {
  display: block;
  margin-bottom: 6px;
  color: #8b5a4f;
}

.resumo-card strong {
  font-size: 1.4rem;
  color: #7c2d12;
}

.layout {
  display: grid;
  grid-template-columns: 320px 1fr;
  gap: 24px;
  align-items: start;
}

.painel-direito {
  display: grid;
  gap: 24px;
}

@media (max-width: 900px) {
  .layout,
  .resumo {
    grid-template-columns: 1fr;
  }
}
</style>
