<template>
    <div>
        <h1> This is Index.Vue </h1><hr>
        <ul>
            <li v-for="profile in this.profiles" v-bind:key="profile.id" class="bg-info text-monospace p-3 m-3">
                {{ profile.id }} <br> {{ profile.name }} <br> {{ profile.email }} <br> {{ profile.age }}
            
                
                
                <button type="submit" class="btn btn-danger ml-auto" v-on:click="del(profile.id)">Delete </button>
                
                <form @submit.prevent="del(profile.id)">
                    <input type="hidden" name="_method" value="DELETE">
                    <button type="submit" class="btn btn-danger ml-5">Delete </button>
                </form>
            </li>
        </ul>
        <small>eof index</small>
    </div>
</template>

<script>
export default {
    name: 'index',
    data(){
        return {
            profiles: '',
            name: '',
            age: '',
            email: ''
        }
    },
    beforeMount: async function() {
        
        this.profiles = await axios.get('http://127.0.0.1:8000/profile')
            .then(function(resp) {
                return resp.data;
            })
            .catch(err => console.log(err));
    },
    methods: {
        async del(id) {

            let response = await axios.delete("http://127.0.0.1:8000/profile/"+id, {
                data: {
                    'id': this.id
                }
            })
            .then(function(resp) {
                console.log(resp)
            })
            .catch(err => console.log(err))

        },
        async updat(id, name, age, email) {

            let response = await axios.put("http://127.0.0.1:8000/profile/"+id, {
                data: {
                    'id': id,
                    'name': name,
                    'age': age,
                    'email': email
                }
            })
            .then(function(resp) {
                console.log(resp)
            })
            .catch(err => console.log(err))

        }
    }
}

</script>