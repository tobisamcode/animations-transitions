<template>
    <ul>
        <li v-for="user in users" :key="user" @click="removeUser(user)"> {{ user }}</li>
    </ul>

    <div>
        <input type="text" ref="userNameInput" >
        <button @click="addUser">Add User</button>
    </div>
</template>



<script>
export default {
    data() {
        return{
            users:['Tobi', 'Banji', 'Subomi', 'Grace', 'Micheal', 'Margeret', 'Raman']
        }
    },
    methods: {
        addUser() {
            const enteredUserName = this.$refs.userNameInput.value;
            this.users.unshift(enteredUserName);
        },
        removeUser(user) {
            this.users = this.users.filter(usr => usr !== user);
        }
    }
}
</script>




<style scoped>

ul {
    margin: 1rem 0;
    padding: 0;
}

ul li {
    border: 1px solid #ccc;
    padding: 1rem;
    text-align: center;
    cursor: pointer ;
}
</style>