<template>
    
    <transition-group tag="ul" name="user-list">
        <li v-for="user in users" :key="user" @click="removeUser(user)"> {{ user }}</li>    
    </transition-group>


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

.user-list-enter-from{
    opacity: 0;
    transform: translateX(-30px);
}

.user-list-enter-active{
    transition: all 1s ease-out;
}

.user-list-leave-active{
    transition: all 1s ease-in;
    position: absolute;
}

.user-list-enter-to
.user-list-leave-from{
    opacity: 1;
    transform: translateX(0);
}

.user-list-leave-from{
    opacity: 0;
    transform: translateX(30px);
}
    
.user-list-move {
    transition: transform .8s ease;
}


</style>