<template>
    <div class="container-fluid">
        <div class="col-12">
           <h1>List Product</h1>           
       </div>
       <form>
           <div class="form-row">
            <div class="form-group col-md-4">
                <input  v-model="code"  class="form-control" placeholder="Search for CODE">       
            </div>
            <div class="form-group col-md-4">
                <button type="button" @click="searchProduct" class="btn btn-success col-4">Search</button>
            </div>
           </div> 
        </form>
        <div v-if="searchProducts != '' " class="table-responsive-md">
            <table  class="table table-hover table-dark">
                <thead>
                    <tr>
                    <th scope="col-6">Category</th>
                    <th scope="col-6">Code</th>
                    <th scope="col-6">Description</th>
                    <th scope="col-6">Price</th>
                    <th scope="col-6">Stock</th>
                    <th><i class="far fa-trash-alt"></i></th>
                    <th><i class="far fa-edit"></i></th>
                    </tr>
                </thead>
                <tbody v-for="oneProduct in searchProducts" :key="oneProduct.id">
                    <tr>
                    <td scope="col-6">{{oneProduct.category.description}}</td>
                    <td scope="col-6">{{oneProduct.codigo}}</td>
                    <td scope="col-6">{{oneProduct.description}}</td>
                    <td scope="col-6">{{oneProduct.price}}</td>
                    <td scope="col-6">{{oneProduct.stock}}</th>
                    <td scope="row"><button  class="btn btn-success">Delete</button></td>
                    <td scope="row"><button  class="btn btn-success">Update</button></td>
                    </tr>
                </tbody>
            </table>
        </div> 
         <div v-else class="table-responsive-md">
            <table  class="table table-hover table-dark">
                <thead>
                    <tr>
                    <th scope="col-6">Category</th>
                    <th scope="col-6">Code</th>
                    <th scope="col-6">Description</th>
                    <th scope="col-6">Price</th>
                    <th scope="col-6">Stock</th>
                    <th><i class="far fa-trash-alt"></i></th>
                    <th><i class="far fa-edit"></i></th>
                    </tr>
                </thead>
                <tbody v-for="listProduc in arrayProduct" :key="listProduc.id">
                    <tr>
                    <td scope="col-6">{{listProduc.category.description}}</th>
                    <td scope="col-6">{{listProduc.codigo}}</td>
                    <td scope="col-6">{{listProduc.description}}</td>
                    <td scope="col-6">{{listProduc.price}}</td>
                    <td scope="col-6">{{listProduc.stock}}</th>
                    <td scope="row"><button @click="DeleteProduct(listProduc.id)" class="btn btn-success">Delete</button></td>
                    <td scope="row"><button  class="btn btn-success">Update</button></td>
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
            arrayProduct : [],
            searchProducts: [],
            code:''
        }
    },
    methods: {
        ListProduct () {
            const app = this
            axios.get('http://localhost:8000/api/product').then(function (response){
                app.arrayProduct = response.data.Category
                console.log(app.arrayProduct)
            })
        },
        DeleteProduct (id) {
            const app = this
            axios.delete('http://localhost:8000/api/product/' + id).then(function (response){
                console.log(response.data)
                 if (response.status == 200) {    
                    app.$toastr.success("Se elimino correctamente", {
                        theme: "bubble",
                        position: "top-center",
                        duration: 3000
                    })
                    app.ListProduct ()
                }
            })
        },
        searchProduct () {
            const app = this
            const product = {
                codigo : app.code
            }
            if ( app.code != '') {
                 axios.post('http://localhost:8000/api/searchProduct/',product).then(function (response){
                    app.searchProducts = response.data.Category
                    console.log(app.searchProducts)
                })
            }
        }
    },
    mounted() {
        this.ListProduct()
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