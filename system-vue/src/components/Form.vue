<template>
   <div id="form">
      <div class="container">
         <div class="row">
           <div class="col-md-8">
             <table class="table table-striped">
               <thead>
                 <tr>
                   <th scope="col">id</th>
                   <th scope="col">name</th>
                   <th scope="col">email</th>
                   <th scope="col">phone</th>
                   <th scope="col">address</th>
                   <th width="130">Actions</th>
                 </tr>
                </thead>
                <tbody>
                  <tr v-for="item in itens" v-bind:key="item.id">
                    <td>{{ item.id }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.email }}</td>
                    <td>{{ item.phone }}</td>
                    <td>{{ item.address }}</td>
                    <td class="text-center">
                      <button @click="edit(itens)" class="btn btn-warning btn-sm">Edit</button>
                      <button @click="destroy(itens)" class="btn btn-danger btn-sm">Trash</button>
                    </td>
                  </tr>
                </tbody>
            </table>
            </div>
            <div class="col-md-4">
              <form>
                <div class="form-group">
                  <label>id</label>
                  <input type="text" v-model="input.id" class="form-group">
                </div>
                <div class="form-group">
                  <label>name</label>
                  <input type="text" v-model="input.name" class="form-group">
                </div>
                <div class="form-group">
                  <label>email</label>
                  <input type="text" v-model="input.email" class="form-group">
                </div>
                <div class="form-group">
                  <label>phone</label>
                  <input type="tel" v-model="input.phone" class="form-group">
                </div>
                <div class="form-group">
                  <label>address</label>
                  <textarea class="form-group" v-model="input.address"></textarea>
                </div>
                <button v-if="savebtn" @click.prevent="save" class="btn btn-primary">Save</button>
                <button v-if="updatebtn" @click.prevent="update(input.id)" class="btn btn-primary">Update</button>
                <button @click.prevent="clear" class="btn btn-primary">Clear</button>
              </form>          
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Form',
  data () {
    return {
      itens : [],
      input: {
        id: '',
        name: '',
        email: '',
        phone: '',
        address: ''
      },
      savebtn: true,  
      updatebtn: false  
    }
  },
  created: function (){
    this.view()
  },
  methods: {
    view: function (){
      this.itens = [
        { id: "1", name: "Johnny", email: "j9j@hotmail.com", phone: "99999-9999", address : "jj" }, 
        { id: "2", name: "Johnny", email: "j9j@hotmail.com", phone: "99999-9999", address : "jj" }, 
        { id: "3", name: "Johnny", email: "j9j@hotmail.com", phone: "99999-9999", address : "jj" }
      ]
    },
    save: function (){
      var id = this.input._id
      var nm = this.input.name
      var em = this.input.email
      var pn = this.input.phone
      var ad = this.input.address

      //add in list itens
      this.items.push({id: _id, name: nm, email: em, phone: pn, address: ad})
      this.clear()

      swal('Added', 'Berhasil tambah data', 'success')
    },
    clear: function (){
      this.savebtn = true
      this.updatebtn = false

      this.input.id = ''
      this.input.name = ''
      this.input.email = ''
      this.input.phone = ''
      this.input.address = ''
    },
    edit: function (item) {
      this.savebtn = false
      this.savebtn = true

      this.input.id = item._id
      this.input.name = item.name
      this.input.email = item.email
      this.input.phone = item.phone
      this.input.address = item.address
    },
    update: function (id) {
      var myid = id - 1
      Object.assign(this.itens[myid], this.input)
      
      var nm = this.input.name
      var em = this.input.email
      var pn = this.input.phone
      var ad =this.input.address

      this.clear()
      swal('Updated', 'Berhasil mengubah data', 'warning')
    },
    destroy: function (item) {
      var del = this.itens.indexOf(item)
      swal({
        title: 'Deleted',
        text: 'Are you sure',
        icon: 'error',
        buttons: true,
        dangerMode: true
      }).then((willDelete) => {
          if(willDelete){
            this.itens.splice(del, 1)
          } else{

          }
      })
    }
  }
}
</script>
