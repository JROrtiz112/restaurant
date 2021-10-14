<template>
    <Header/>
    <h1>Hello User, Welcome to Add Restaurant page.</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter name..." v-model="restaurant.name">
        <input type="text" name="name" placeholder="Enter address..." v-model="restaurant.address">
        <input type="text" name="contact" placeholder="Enter contact..." v-model="restaurant.number">
        <button type="button" v-on:click="addRestaurant">Add new Restaurant</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default{
    name: 'Add',
    data(){
        return{
            restaurant:{
                name:'',
                address:'',
                number:'',
            }
        }
    },
    components:{
        Header,
    },
    methods:{
        async addRestaurant(){
            const result = await axios.post("http://localhost:3000/restaurants",{
                name: this.restaurant.name,
                address: this.restaurant.address,
                number: this.restaurant.number,
            });
            console.warn("result",result);
            if (result.status == 201){
                this.$router.push({name:'Home'})
            }
        }
    },
    mounted(){
        let user = localStorage.getItem('user-info');
        if (!user){
            this.$router.push({name:'SignUp'});
        }
    },
}
</script>
