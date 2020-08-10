<template>
    <div>
        <h1> This is Update.Vue </h1><hr>
            
                
                <form @submit.prevent="updat(id, name, age, email)">
                    <input type="hidden" name="_method" value="PUT">
                    <input type="text" v-model="id" value="profile.id">
                    <input type="text" v-model="name" value="profile.name">
                    <input type="text" v-model="age" value="profile.age">
                    <input type="text" v-model="email" value="profile.email">
                    <button type="submit" class="btn btn-warning ml-5">Update </button>
                </form>
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


