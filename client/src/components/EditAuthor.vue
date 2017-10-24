<template>
<div class="addauthor">
  <div class="err_info">{{errEdit}}</div>
  <div class="add_info">{{isEdit}}</div>
  <div class="add">
    <div class="lbl_add">Author(id:{{author.id}}) edit form</div>
      <p class="bg-danger" id="err" style="width: 100%">{{err_author}}</p>
      <div class="form-group">
        <label for="inputName">Name</label>
        <input type="text" class="form-control" id="inputName" placeholder="Enter name" v-model="author.name">
      </div>
      <div class="form-group">
        <label for="inputSname">Surname</label>
        <input type="text" class="form-control" id="inputSname" placeholder="Enter surname" v-model="author.surname">
      </div>
      <button  class="btn btn-primary"  @click="edit_author">Edit author</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'addAuthor',
  data () {
    return {
      err_Edit: "",
      isEdit: "",
      author: {},
      author_show: true
    }
  },
  created(){
   
  },
  methods:{
    edit_author(){}
  },
   computed:{
    author_id: function(){
      var id = this.$route.params.id
      //alert(this.$route.params.id)
      var self = this
      //axios.get('http://localhost:88/BOOK_SHOP/client/api/author/'+ this.$route.params.id, this.config)
      axios.get('http://192.168.0.15/~user15/BOOK_SHOP/client/api/author/'+  this.$route.params.id, this.config)
            .then(function (response) {
              //console.log(response.data)
              self.author = response.data.data
               //console.log(temp)
              if( self.author.length == 0){
                self.errEdit = "Information about this author is absent"
                self.author_show = false
              }
            })
            .catch(function (error) {
              self.errEdit = "Information about this author is absent"
              self.author_show = false

          }); 
      return id;
    }
   }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
