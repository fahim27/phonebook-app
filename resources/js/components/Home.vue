<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">
                        <div class="row">
                            <div class="col-lg-6">
                        <h3>Phonebook</h3>

                            </div>
                            <div class="col-lg-4"></div>
                            <div class="col-lg-2">
                        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#addModal"><i class="fa fa-plus"></i></button>

                            </div>
                        </div>
                    </div>

                    <div class="card-body">
                       <div class="main-content">
                           <div class="row" v-for="item,key in lists">
                               <div class="col-lg-10">
                           <P>{{item.name}}</P>

                               </div>
                               <div class="col-lg-2">
                           <i class="fa fa-eye" @click="showItem(key)"></i>
                           <i class="fa fa-edit" @click="update(key)"></i>
                           <i class="fa fa-trash" @click="del(key,item.id)"></i>



                               </div>
                           </div>

                       </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- Button trigger modal -->

<!-- Modal -->
<div class="modal fade" id="addModal" tabindex="-1" role="dialog" aria-labelledby="addModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Add Contact</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
    
  <div class="form-group">
    <label>Name</label>
    <input type="text" class="form-control" v-model="list.name" placeholder="Enter Name" name="name">
	<small v-if="errors.name" class="text-danger">{{ errors.name[0] }}</small>

  </div>

  <div class="form-group">
    <label>Phone</label>
    <input type="text" class="form-control" v-model="list.phone" placeholder="Enter Name" name="phone">
		<small v-if="errors.name" class="text-danger">{{ errors.name[0] }}</small>

  </div>

  <div class="form-group">
    <label>Email</label>
    <input type="email" class="form-control" v-model="list.email" placeholder="Enter email" name="email">
		<small v-if="errors.name" class="text-danger">{{ errors.name[0] }}</small>

  </div>
  
 
  <button  class="btn btn-primary" style="width:100%;" @click="save" >Submit</button>
 
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
<Show></Show>
<Update></Update>
    </div>


</template>

<script>
 Vue.component('Show', require('./Show.vue').default);
 Vue.component('Update', require('./Update.vue').default);

    export default {
       data(){
           return {
               list:{
                   name:"",
                   phone:"",
                   email:""
               },
			   errors:{},
			   lists:{}
           }
       },
	    mounted() {
            axios.get('/phonebook')
               .then((response)=> this.lists=response.data)
				  .catch((error) => console.log(error))
        },
       methods: {
           save(){
               axios.post('/phonebook',this.$data.list)
               .then((response)=>{
			   this.lists.push(response.data);
			   $('#addModal').modal('hide')
			   })
				.catch((error) => {
				this.errors=error.response.data.errors
				})
           },
		   showItem(key){
		     this.$children[0].list=this.lists[key];
		   			   $('#showModal').modal('show');

		   },
		   update(key){
		   		     this.$children[1].list=this.lists[key];

		   			   $('#updateModal').modal('show');

		   },
		   del(key,id){
		     if(confirm("are you sure delete this item")){
			 axios.delete(`/phonebook/${id}`)
					.then((response)=> {this.lists.splice(key,1);})
					.catch((error) => this.errors = error.response.data.errors)	
			 }
		   }
		  
       }
    }
</script>
