<script setup>
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
</script>

<template>
    <button v-if="$page.props.user.permissions.includes('create roles')">Create Roles</button>
    <button v-is="$page - props.user.permissions.includes('create lessons')">Create new Lessons</button>
</template>

<style>
button {
    background: green;
    color: white;
    padding: 20px;
    margin: 5px;
}
</style>
