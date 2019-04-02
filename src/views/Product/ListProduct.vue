<template>
    <div class="container-fluid">
        <div class="col-12">
           <h1>List Product</h1>           
       </div>
         <div  class="table-responsive-md">
            <table class="table table-hover table-dark">
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
                <tbody >
                    <tr>
                    <td scope="col-6">Category</th>
                    <td scope="col-6">Code</td>
                    <td scope="col-6">Description</td>
                    <td scope="col-6">Price</td>
                    <td scope="col-6">Stock</th>
                    <td scope="row"><button  class="btn btn-success">Delete</button></td>
                    <td scope="row"><button  class="btn btn-success">Update</button></td>
                    </tr>
                </tbody>
            </table>
        </div> 
    </div>
</template>
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
</style>