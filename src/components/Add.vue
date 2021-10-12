<template>
  <div class="add container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Add Person</h1>
    <form v-on:submit="addCustomer">
        <div class="well">
            <h4>Person Info</h4>
            <div class="form-group">
                <label>ID</label>
                <input type="text" class="form-control" placeholder="ID" v-model="customer.id">
            </div>
            <div class="form-group">
                <label>First Name</label>
                <input type="text" class="form-control" placeholder="First Name" v-model="customer.first_name">
            </div>
            <div class="form-group">
                <label>Last Name</label>
                <input type="text" class="form-control" placeholder="Last Name" v-model="customer.last_name">
            </div>
             <div class="form-group">
                <label>Email</label>
                <input type="text" class="form-control" placeholder="Email" v-model="customer.email">
            </div>
        </div>
       

        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
    import Alert from './Alert'
    export default {
    name: 'add',
    data () {
        return {
        customer: {},
        alert:''
        }
    },
    methods: {
        addCustomer(e){
            if(!this.customer.first_name || !this.customer.last_name || !this.customer.email){
                this.alert = 'Please fill in all required fields';
            } else {
                let newCustomer = {
                     id: this.customer.id,
                    first_name: this.customer.first_name,
                    last_name: this.customer.last_name,
                    email: this.customer.email,
                   
                }

                this.$http.post('http://slimapp/api/customer/add', newCustomer)
                    .then(function(response){
                        this.$router.push({path: '/', query: {alert: 'Customer Added'}});
                    });

                e.preventDefault();
            }
            e.preventDefault();
        }
    },
    components: {
        Alert
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
