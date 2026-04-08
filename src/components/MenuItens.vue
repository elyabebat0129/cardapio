<script setup>
defineProps({
  itens: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['remove-item'])
</script>

<template>
  <section class="bloco">
    <h2>Lista de itens</h2>

    <div v-if="itens.length" class="lista-itens">
      <article
        v-for="item in itens"
        :key="item.id"
        class="card"
        :class="{ indisponivel: !item.disponivel }"
      >
        <div class="topo-card">
          <span class="categoria">{{ item.categoria }}</span>
          <span class="status">{{ item.disponivel ? 'Disponivel' : 'Indisponivel' }}</span>
        </div>

        <h3>{{ item.nome }}</h3>
        <p class="preco">R$ {{ item.preco.toFixed(2) }}</p>
        <p>Categoria: {{ item.categoria }}</p>
        <p>Disponivel: {{ item.disponivel ? 'Sim' : 'Nao' }}</p>

        <button @click="emit('remove-item', item.id)">Remover</button>
      </article>
    </div>

    <p v-else class="vazio">Nenhum item encontrado nesse filtro.</p>
  </section>
</template>

<style scoped>
.bloco {
  margin-bottom: 24px;
}

h2 {
  margin-top: 0;
  margin-bottom: 16px;
}

.lista-itens {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
}

.card {
  padding: 18px;
  border: 1px solid #f0d0bd;
  border-radius: 18px;
  background: #fffdfb;
  box-shadow: 0 10px 24px rgba(88, 45, 32, 0.08);
}

.topo-card {
  display: flex;
  justify-content: space-between;
  gap: 8px;
  margin-bottom: 14px;
  flex-wrap: wrap;
}

.categoria,
.status {
  padding: 6px 10px;
  border-radius: 999px;
  font-size: 0.85rem;
  font-weight: 700;
}

.categoria {
  background: #ffedd5;
  color: #9a3412;
}

.status {
  background: #ede9fe;
  color: #5b21b6;
}

h3 {
  margin: 0 0 8px;
}

.preco {
  margin: 0 0 10px;
  font-size: 1.2rem;
  font-weight: 700;
  color: #7c2d12;
}

button {
  border: 0;
  border-radius: 12px;
  padding: 10px 14px;
  font-weight: 700;
  color: #fff;
  background: #7f1d1d;
  cursor: pointer;
}

.indisponivel {
  opacity: 0.6;
}

.indisponivel h3,
.indisponivel .preco {
  text-decoration: line-through;
}

.vazio {
  padding: 20px;
  border-radius: 16px;
  background: #fffdfb;
  border: 1px dashed #d9b7a4;
}
</style>
