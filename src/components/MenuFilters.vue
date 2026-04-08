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
  <section class="bloco">
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

.filtros {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}

.ativo {
  background: #222;
  color: #fff;
}
</style>
