<template>
    <Header/>
    <h1>Hello User, welcome to Update Restaurant page.</h1>
    <form class="update">
        <input type="text" name="name" placeholder="Enter name..." v-model="restaurant.name">
        <input type="text" name="name" placeholder="Enter address..." v-model="restaurant.address">
        <input type="text" name="contact" placeholder="Enter contact..." v-model="restaurant.number">
        <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default{
    name: 'Update',
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
        async updateRestaurant(){
            const result = await axios.put("http://localhost:3000/restaurants/"+this.$route.params.id,{
                name: this.restaurant.name,
                address: this.restaurant.address,
                number: this.restaurant.number,
            });
            console.warn("result",result);
            if (result.status == 200){
                this.$router.push({name:'Home'})
            }
        }
    },
    async mounted(){
        let user = localStorage.getItem('user-info');
        if (!user){
            this.$router.push({name:'SignUp'});
        }

        const result = await axios.get('http://localhost:3000/restaurants/'+this.$route.params.id )
        if (result.status == 200){
            this.restaurant = result.data
        }
        console.warn(result); 
    },
}
</script>
