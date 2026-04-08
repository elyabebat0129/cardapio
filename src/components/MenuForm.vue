<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['add-item'])

const form = reactive({
  nome: '',
  preco: null,
  categoria: 'Lanche',
  disponivel: true,
})

const resetarFormulario = () => {
  form.nome = ''
  form.preco = null
  form.categoria = 'Lanche'
  form.disponivel = true
}

const enviarFormulario = () => {
  emit('add-item', {
    nome: form.nome.trim(),
    preco: Number(form.preco),
    categoria: form.categoria,
    disponivel: form.disponivel,
  })

  resetarFormulario()
}
</script>

<template>
  <section class="bloco card-form">
    <h2>Cadastro de itens</h2>

    <form class="formulario" @submit.prevent="enviarFormulario">
      <input v-model="form.nome" type="text" placeholder="Nome do item" required />

      <input
        v-model.number="form.preco"
        type="number"
        min="0"
        step="0.01"
        placeholder="Preco"
        required
      />

      <select v-model="form.categoria">
        <option value="Lanche">Lanche</option>
        <option value="Bebida">Bebida</option>
        <option value="Sobremesa">Sobremesa</option>
      </select>

      <label class="checkbox">
        <input v-model="form.disponivel" type="checkbox" />
        Disponivel
      </label>

      <button type="submit">Adicionar item</button>
    </form>
  </section>
</template>

<style scoped>
.bloco {
  margin-bottom: 24px;
}

.card-form {
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

.formulario {
  display: grid;
  gap: 12px;
}

input,
select,
button {
  font: inherit;
}

input,
select {
  width: 100%;
  padding: 12px 14px;
  border: 1px solid #e5c9b6;
  border-radius: 12px;
  background: #fff;
}

.checkbox {
  display: flex;
  gap: 8px;
  align-items: center;
  font-weight: 600;
}

.checkbox input {
  width: auto;
}

button {
  border: 0;
  border-radius: 12px;
  padding: 12px 16px;
  font-weight: 700;
  color: #fff;
  background: #c2410c;
  cursor: pointer;
}
</style>
