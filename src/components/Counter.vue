<template>
  <div class="counter">
    <button @click="decrement" class="counter-btn minus">-</button>
    <span class="counter-value">{{ count }}</span>
    <button @click="increment" class="counter-btn plus">+</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  initial: {
    type: Number,
    default: 0
  }
});

const emit = defineEmits(['change']);

const count = ref(props.initial);

const increment = () => {
  count.value++;
  emit('change', count.value);
};

const decrement = () => {
  count.value--;
  emit('change', count.value);
};
</script>

<style scoped>
.counter {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: #2a2a2a;
  padding: 0.5rem 1rem;
  border-radius: 8px;
}

.counter-btn {
  width: 32px;
  height: 32px;
  border: none;
  border-radius: 6px;
  font-size: 1.2rem;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.minus {
  background: #3a3a3a;
  color: #e0e0e0;
}

.minus:hover {
  background: #4a4a4a;
}

.plus {
  background: #646cff;
  color: white;
}

.plus:hover {
  background: #535bf2;
}

.counter-value {
  font-size: 1.5rem;
  font-weight: bold;
  min-width: 2rem;
  text-align: center;
  color: #e0e0e0;
}
</style>
