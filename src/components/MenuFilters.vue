<script setup>
defineProps({
  categorias: {
    type: Array,
    required: true,
  },
  filtroAtual: {
    type: String,
    required: true,
  },
})

const emit = defineEmits(['change-filter'])
</script>

<template>
  <section class="bloco card-filtros">
    <h2>Filtros</h2>

    <div class="filtros">
      <button
        v-for="categoria in categorias"
        :key="categoria"
        :class="{ ativo: filtroAtual === categoria }"
        @click="emit('change-filter', categoria)"
      >
        {{ categoria }}
      </button>
    </div>
  </section>
</template>

<style scoped>
.bloco {
  margin-bottom: 24px;
}

.card-filtros {
  padding: 20px;
  border-radius: 18px;
  background: #fffdfb;
  border: 1px solid #f3d4bf;
  box-shadow: 0 10px 24px rgba(88, 45, 32, 0.08);
}

h2 {
  margin-top: 0;
  margin-bottom: 16px;
}

.filtros {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}

button {
  border: 1px solid #e5c9b6;
  border-radius: 999px;
  padding: 10px 14px;
  background: #fff7f1;
  color: #7c2d12;
  cursor: pointer;
}

.ativo {
  background: #7c2d12;
  border-color: #7c2d12;
  color: #fff;
}
</style>
