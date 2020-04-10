<template>

<!-- Modal -->
<div class="modal fade" id="showModal" tabindex="-1" role="dialog" aria-labelledby="showModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Show Contact</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
	  <h4>Name:</h4>
	  <h4>{{list.name}}</h4>
	  <br/>
	  <h4>Phone:</h4>
	  <h4>{{list.phone}}</h4>
	  <br/>
	  <h4>Email:</h4>
	  <h4>{{list.email}}</h4>
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
		list:''
	 }
  },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>