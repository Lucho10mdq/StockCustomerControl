<template>
    <div class="container-fluid">
        <div class="col-12">
           <h1>List Customer</h1>           
       </div>
       <form>
           <div class="form-row">
            <div class="form-group col-md-4">
                <input  v-model="dni"  class="form-control" placeholder="Search for DNI">       
            </div>
            <div class="form-group col-md-4">
                <button type="button" @click="searchCustomers" class="btn btn-success col-4">Search</button>
            </div>
           </div> 
       </form>
       <div  v-if="searchCustomer != '' " class="table-responsive-md">
           <table class="table table-hover table-dark">
                <thead>
                    <tr>
                    <th scope="col-6">Nro Customer</th>
                    <th scope="col-6">Name</th>
                    <th scope="col-6">LastName</th>
                    <th scope="col-6">Dni</th>
                    <th scope="col-6">Addres</th>
                    <th scope="col-6">Email</th>
                    <th scope="col-6">Phone</th>
                    <th><i class="far fa-trash-alt"></i></th>
                    <th><i class="far fa-edit"></i></th>
                    </tr>
                </thead>
                <tbody >
                    <tr>
                    <td scope="row">{{searchCustomer.nro_customer}}</td>
                    <td scope="row">{{searchCustomer.name}}</td>
                    <td scope="row">{{searchCustomer.lastname}}</td>
                    <td scope="row">{{searchCustomer.dni}}</td>
                    <td scope="row">{{searchCustomer.address}}</td>
                    <td scope="row">{{searchCustomer.email}}</td>
                    <td scope="row">{{searchCustomer.phone}}</td>
                    <td scope="row"><button @click="DeleteCustomer(searchCustomer.id)" class="btn btn-success">Delete</button></td>
                    <td scope="row"><button  class="btn btn-success">Update</button></td>
                    </tr>
                </tbody>
            </table>
        </div>   
        <div v-else class="table-responsive-md">
            <table class="table table-hover table-dark">
                <thead>
                    <tr>
                    <th scope="col-6">Nro Customer</th>
                    <th scope="col-6">Name</th>
                    <th scope="col-6">LastName</th>
                    <th scope="col-6">Dni</th>
                    <th scope="col-6">Addres</th>
                    <th scope="col-6">Email</th>
                    <th scope="col-6">Phone</th>
                    <th><i class="far fa-trash-alt"></i></th>
                    <th><i class="far fa-edit"></i></th>
                    </tr>
                </thead>
                <tbody v-for="Customers in listCustomers" :key="Customers.id">
                    <tr>
                    <td scope="row">{{Customers.nro_customer}}</td>
                    <td scope="row">{{Customers.name}}</td>
                    <td scope="row">{{Customers.lastname}}</td>
                    <td scope="row">{{Customers.dni}}</td>
                    <td scope="row">{{Customers.address}}</td>
                    <td scope="row">{{Customers.email}}</td>
                    <td scope="row">{{Customers.phone}}</td>
                    <td scope="row"><button @click="DeleteCustomer(Customers.id)" class="btn btn-success">Delete</button></td>
                    <td scope="row"><button @click="EditCustomers(Customers.id)" class="btn btn-success">Update</button></td>
                    </tr>
                </tbody>
            </table>
        </div>    
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data () {
        return {
            listCustomers : [],
            dni:'',
            searchCustomer: []
        }
    },
    methods: {
        listCustomer () {
            const app = this
            axios.get('http://localhost:8000/api/customer').then(function (response){
                app.listCustomers = response.data.Customer
                console.log(app.listCustomers)
            })
        },
        DeleteCustomer (id) {
            const app = this
            axios.delete('http://localhost:8000/api/customer/' + id).then(function (response){
                if (response.status == 200) {    
                    app.$toastr.success("Se elimino correctamente", {
                        theme: "bubble",
                        position: "top-center",
                        duration: 3000
                    })
                    app.listCustomer ()
                }
            })
        },
        searchCustomers () {
            const app =this
            const customer = {
                dni: app.dni
            }
            if (app.dni != ''){
                axios.post('http://localhost:8000/api/customerSearch/',customer).then(function (response){
                    app.searchCustomer = response.data.Customer
                    console.log(app.searchCustomer)
                })
            } else {
                app.$toastr.error("Debe ingresar el dni", {
                    theme: "bubble",
                    position: "top-center",
                    duration: 3000
                })
            } 
        },
         EditCustomers (id) {
            this.$router.push('/edit_client/' + id)
         }
    },
    mounted() {
        this.listCustomer()
    },
}
</script>
<style>
h1 {
      margin-left: auto;
      margin-right: auto;
      margin-top: 4%;
     text-align: center;
 }
 .table {
    width: 100%;
    margin-bottom: 1rem;
    /*color: #212529;*/
    margin-top: 2%;
}
.form-control {
    display: block;
    width: 100%;
    height: calc(1.5em + .75rem + 2px);
    padding: .375rem .75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: .25rem;
    transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    margin-top: 5%;
}
.btn {
    display: inline-block;
    font-weight: 400;
    /*color: #212529;*/
    text-align: center;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    /*background-color: transparent;*/
    border: 1px solid transparent;
       /* border-top-color: transparent;
        border-right-color: transparent;
        border-bottom-color: transparent;
        border-left-color: transparent;*/
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: .25rem;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    margin-top: 5%;
}
</style>

