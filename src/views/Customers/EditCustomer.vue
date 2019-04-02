<template>
    <div class="container-fluid">
       <div class="col-12">
           <h1>Edit Customer</h1>           
       </div> 
       <form>
          <div class="form-row">
           <div class="form-group col-md-4">
               <input  v-model="name"  class="form-control" placeholder="Name">
           </div>
           <div class="form-group col-md-4">
               <input  v-model="lastName"  class="form-control" placeholder="LastName">
           </div>
           <div class="form-group col-md-4">
               <input  v-model="dni"  class="form-control" placeholder="Dni">
           </div>
           <div class="form-group col-md-4">
               <input  v-model="address"  class="form-control" placeholder="Address">
           </div>
           <div class="form-group col-md-4">
               <input  v-model="phone"  class="form-control" placeholder="Phone">
           </div>
           <div class="form-group col-md-4">
               <input  v-model="email"  class="form-control" placeholder="Email">
           </div>
           <div class="form-group col-md-4">
               <input  v-model="nro_customer"  class="form-control" placeholder="Number Clustomer">
           </div>
          </div>      
       </form> 
       <loading :active.sync="isLoading" 
        :can-cancel="true" 
        :is-full-page="fullPage"></loading>
       <button v-on:click="updateCustomer" class="col-md-4 btn btn-success">Save</button>
    </div>
</template>
<script>
import axios from 'axios'
import Loading from 'vue-loading-overlay';
    // Import stylesheet
import 'vue-loading-overlay/dist/vue-loading.css';
export default {
    data () {
        return {
            name: '',
            lastName: '',
            dni: '',
            address: '',
            phone: '',
            email: '',
            nro_customer:'',
            isLoading: false,
            fullPage: true
        }
    },
    components: {
        Loading
    },
    methods: {
        editCustomer () {
            const app = this
            const id = this.$route.params.id
            console.log('llegue')
            axios.get('http://localhost:8000/api/customer/' + id ).then(function (response){
                app.name = response.data.Customer.name
                app.lastName = response.data.Customer.lastname
                app.dni = response.data.Customer.dni
                app.address = response.data.Customer.address
                app.phone = response.data.Customer.phone
                app.nro_customer = response.data.Customer.nro_customer
                app.email = response.data.Customer.email
            })          
        },
        updateCustomer  () {
            const app = this
             app.isLoading = true;
             const id = this.$route.params.id
            const customer = {
                name: app.name,
                lastname: app.lastName,
                address: app.address,
                dni: app.dni,
                phone: app.phone,
                email: app.email,
                nro_customer: app.nro_customer
            }
            if ((app.name != '' ) && (app.lastname != '') && (app.dni != '' ) && (app.address != '') && (app.phone != '') && (app.email != '') && (app.nro_customer != '')){
                 app.isLoading = true;
                 axios.put('http://localhost:8000/api/customer'+ id, customer).then(function (response){
                    console.log(response)
                    if (response.status == 200){
                        console.log("hola")
                        app.$toastr.success("Se agrego correctamente", {
                            theme: "bubble",
                            position: "top-center",
                            duration: 3000
                        })
                        this.isLoading = false
                        app.name = '',
                        app.lastname = '',
                        app.dni = '',
                        app.email = '',
                        app.phone = '',
                        app.address = '',
                        app.nro_customer = ''
                    } else {
                        console.log('enmtre')
                        app.$toastr.error("El dni ya existe !!", {
                            theme: "bubble",
                            position: "top-center",
                            duration: 3000
                        })
                    }
                }).catch ( e => {
                    app.$toastr.error('Servidor no encontrado', {
                        theme: "bubble",
                        position: "top-center",
                        duration: 3000
                        })
                        this.isLoading = false
                    })
            }
            else {
                app.$toastr.error("No pueden quedar datos vacios !!", {
                    theme: "bubble",
                    position: "top-center",
                    duration: 3000
                })
            }     
        }    
      },
      mounted () {
          this.editCustomer()
      }
    }
</script>

<style>
 h1 {
      margin-left: auto;
      margin-right: auto;
      margin-top: 4%;
     text-align: center;
 }
 button{
     float: none;
     text-align: center;
     margin-left: auto;
    margin-right: auto;
 }
 .form-row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -5px;
    margin-left: -5px;
    margin-top: 4%;
}
</style>
