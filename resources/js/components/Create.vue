<template>
    <div>
        <h1> This is Create.Vue </h1><hr>
        <form @submit.prevent="send">
            
            <div class="form-group">
                <label for="name">Name</label>
                <input type="text" v-model="name" name="name">
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <input type="text" v-model="email" name="email">
            </div>
            <div class="form-group">
                <label for="age">Age</label>
                <input type="number" v-model="age" name="age">
            </div>
            <button type="submit">Send </button>

        </form>
        <small>eof create</small>
    </div>
</template>

<script>
export default {
    name: 'create',
    data(){
        return {
            profiles: '',
            name: '',
            age: '',
            email: ''
        }
    },
    methods: {
        async send() {
            let response = await axios.post('http://127.0.0.1:8000/profile', {
                'name': this.name,
                'age': this.age,
                'email': this.email
            })
            .then(function(resp) {
                console.log(resp)
            })
            .catch(err => console.log(err))
        }
    }
}

</script>