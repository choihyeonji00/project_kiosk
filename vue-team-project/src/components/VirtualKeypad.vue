<script setup>

const emit = defineEmits(['input', 'delete', 'clear']);
const keys = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'C', '0', '⌫'];
const handleKey = (key) => {
  if (key === '⌫') emit('delete');
  else if (key === 'C') emit('clear');
  else emit('input', key);
};

</script>
<template>
  <div class="keypad-grid">
    <button v-for="key in keys" :key="key" @click="handleKey(key)" 
            :class="{ 'spec-key': key === 'C' || key === '⌫' }">
      {{ key }}
    </button>
  </div>
</template>
<style scoped>
.keypad-grid { 
    display: grid; 
    grid-template-columns: repeat(3, 1fr); 
    gap: 10px; 
    width: 100%; 
}
button { 
    height: 60px; 
    font-size: 20px; 
    font-weight: bold; 
    border-radius: 8px; 
    border: 1px solid #ccc; 
    background: white; 
    cursor: pointer; 
}
.spec-key {
    background: #f0f0f0; 
}
</style>