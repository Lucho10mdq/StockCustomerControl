<template>
    <div class="container">
        <div class="col-12">
           <h1>List Category</h1>           
       </div>
       <form>
           <div class="form-row">
            <div class="form-group col-md-4">
                <input  v-model="description"  class="form-control" placeholder="Search for description">       
            </div>
            <div class="form-group col-md-4">
                <button type="button" @click="searchCategory" class="btn btn-success col-4">Search</button>
            </div>
           </div> 
       </form>
       <div v-if="searchCategories != '' " class="table-responsive-md">
            <table class="table table-hover table-dark">
                <thead>
                    <tr>
                    <th scope="col-6">Id</th>
                    <th scope="col-6">Description</th>
                    <th><i class="far fa-trash-alt"></i></th>
                    <th><i class="far fa-edit"></i></th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                    <td scope="row">{{searchCategories.id}}</td>
                    <td scope="row">{{searchCategories.description}}</td>
                    <td scope="row"><button @click="DeleteCategory(searchCategories.id)" class="btn btn-success">Delete</button></td>
                    <td scope="row"><button @click="EditCategory(searchCategories.id)" class="btn btn-success">Update</button></td>
                    </tr>
                </tbody>
            </table>
        </div>    
       <div v-else class="table-responsive-md">
            <table class="table table-hover table-dark">
                <thead>
                    <tr>
                    <th scope="col-6">Id</th>
                    <th scope="col-6">Description</th>
                    <th><i class="far fa-trash-alt"></i></th>
                    <th><i class="far fa-edit"></i></th>
                    </tr>
                </thead>
                <tbody v-for="Category in listCategories" :key="Category.id">
                    <tr>
                    <td scope="row">{{Category.id}}</td>
                    <td scope="row">{{Category.description}}</td>
                    <td scope="row"><button @click="DeleteCategory(Category.id)" class="btn btn-success">Delete</button></td>
                    <td scope="row"><button @click="EditCategory(Category.id)" class="btn btn-success">Update</button></td>
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
            listCategories : [],
            description:'',
            searchCategories: []
        }
    },
    methods: {
        listCategory () {
            const app = this
            axios.get('http://localhost:8000/api/category').then(function (response){
                app.listCategories = response.data.Category
                console.log(app.listCategories)
            })
        },
        DeleteCategory (id) {
            const app = this
            axios.delete('http://localhost:8000/api/category/' + id).then(function (response){
                if (response.status == 200) {    
                    app.$toastr.success("Se elimino correctamente", {
                        theme: "bubble",
                        position: "top-center",
                        duration: 3000
                    })
                    app.listCategory ()
                }
            })
        },
        searchCategory () {
            const app =this
            const category = {
                description: app.description
            }
            if (app.description != ''){
                axios.post('http://localhost:8000/api/searchCategory/',category).then(function (response){
                    app.searchCategories = response.data.Category
                    console.log(app.searchCategories)
                })
            } else {
                app.$toastr.error("Debe ingresar la descripcion", {
                    theme: "bubble",
                    position: "top-center",
                    duration: 3000
                })
            } 
        },
         EditCategory (id) {
            this.$router.push('/edit_category/' + id)
         }
    },
    mounted() {
        this.listCategory()
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
