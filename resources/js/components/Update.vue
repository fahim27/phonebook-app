<template>

<!-- Modal -->
<div class="modal fade" id="updateModal" tabindex="-1" role="dialog" aria-labelledby="updateModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title text-center" id="exampleModalLabel">Edit {{list.name}}</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
	 <div class="form-group">
    <label>Name</label>
    <input type="text" class="form-control" v-model="list.name" placeholder="Enter Name" name="name">

  </div>

  <div class="form-group">
    <label>Phone</label>
    <input type="text" class="form-control" v-model="list.phone" placeholder="Enter Name" name="phone">

  </div>

  <div class="form-group">
    <label>Email</label>
    <input type="email" class="form-control" v-model="list.email" placeholder="Enter email" name="email">

  </div>
  
 
  <button  class="btn btn-primary" style="width:100%;" @click="update" >Update</button>
    </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
</template>


<script>
    export default {
	 data(){
     
	 return {
		list:{},
		errors:{}
	 }
  },
  methods:{
    update(){
	axios.patch(`/phonebook/${this.list.id}`,this.$data.list).then((response)=>{
	  $("#updateModal").modal('hide');
	})
				  .catch((error) => this.errors = error.response.data.errors)
			}
	
  },

        mounted() {
            console.log('Component mounted.')
        }
    }
</script>