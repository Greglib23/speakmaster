<script setup>
import { ref } from 'vue';
const emit = defineEmits(['onCategories'])
defineProps({
    collection: {
        type: Array,
        required: true
    }
})
const currentSelection = ref(1)
const selection = ref([])
const handleAddToSelection = () => {
    if (!selection.value.includes(currentSelection.value)) {
        selection.value.push(currentSelection.value)
        emit('onCategories', selection.value)
    }
}
const handleRemoveSelection = (index) => {
    selection.value.splice(index, 1);
    emit('onCategories', selection.value)
}


</script>

<template>
    <select v-model="currentSelection" class="w-4/5 rounded">
        <option v-for="(item, index) in collection" :key="index">{{ item?.name }}</option>
    </select>
    <button @click="handleAddToSelection" class="w-1/5">Add</button>
    <div>
        <ul>
            <li v-for="(item, index) in selection" :key="index">{{ item }}
                <button @click="handleRemoveSelection(index)">Remove</button>
            </li>
        </ul>
    </div>
</template>
