<template>
    <ul>
        <li v-for="user in users" :key="user"> {{ user }} </li>
    </ul>
</template>

<script>
export default {
    data() {
        return{
            users:['Tobi', 'Banji', 'Subomi', 'Grace', 'Micheal', 'Margeret', 'Raman']
        }
    }
}
</script>