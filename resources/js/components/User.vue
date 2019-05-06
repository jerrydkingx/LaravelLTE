<template>
    <div class="container">
<div class="row mt-5">
          <div class="col-md-12">
            <div class="card">
              <div class="card-header">
                <h3 class="card-title">User Table</h3>

                <div class="card-tools">
                    <button class="btn btn-success"  data-toggle="modal" data-target="#addNew"> <div class="fa fa-user-plus"></div> Add New</button>
                </div>  
              </div>
              <!-- /.card-header -->
              <div class="card-body table-responsive p-0">
                <table class="table table-hover">
                  <tbody><tr>
                    <th>ID</th>
                    <th>User</th>
                    <th>Date</th>
                    <th>Type</th>
                    <th>Email</th>
                    <th>Bio</th>
                    <th>Modify</th>
                  </tr>
                  <tr v-for="user in users" :key="user.id">
                    <td>{{user.id}}</td>
                    <td>{{user.name}}</td>
                    <td>{{user.date}}</td>
                    <td>{{user.type}}</td>
                    <td>{{user.email}}</td>
                    <th>{{user.bio}}</th>
                    <td><span class="tag tag-success">{{user.type}}</span></td>
                    <td>
                        <a href="#">
                            <li class="fa fa-edit"></li>
                        </a>
                        <a href="#">
                            <li class="fa fa-trash"></li>
                        </a>
                    </td>
                  </tr>
                </tbody></table>
              </div>
              <!-- /.card-body -->
            </div>
            <!-- /.card -->
          </div>
<div class="modal fade" id="addNew" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Add New</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <form @submit.prevent="userCreate">
      <div class="modal-body">
                <div class="form-group">
                <input v-model="form.name" type="text" name="name" placeholder="Name"
                    class="form-control" :class="{ 'is-invalid': form.errors.has('name') }">
                <has-error :form="form" field="name"></has-error>
                </div> 
                <div class="form-group">
                <input v-model="form.email" type="email" name="email" placeholder="Email"
                    class="form-control" :class="{ 'is-invalid': form.errors.has('email') }">
                <has-error :form="form" field="email"></has-error>
                </div> 
                <div class="form-group">
                <textarea v-model="form.bio" type="bio" name="bio" placeholder="Enter your Bio"
                    class="form-control" :class="{ 'is-invalid': form.errors.has('bio') }">
                </textarea>
                <has-error :form="form" field="bio"></has-error>
                </div> 
                <div class="form-group">
                <select v-model="form.type" type="text" name="type"
                    class="form-control" :class="{ 'is-invalid': form.errors.has('type') }">
                    <option value="">Select User Role</option>
                    <option value="admin">Admin</option>
                    <option value="standard">Standard</option>
                    <option value="user">User</option>
                    <option value="author">Author</option>
                    </select>
                <has-error :form="form" field="type"></has-error>
                </div> 
                <div class="form-group">
                <input v-model="form.password" type="password" name="password"
                    class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
                <has-error :form="form" field="password"></has-error>
                </div>

           
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
        <button type="submit" class="btn btn-primary">Create</button>
      </div>
      </form>
    </div>
  </div>
</div>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
    return {
      users: {

      },
      // Create a new form instance
      form: new Form({
        name: '',
        email: '',
        bio: '',
        type: '',
        password: '',
        remember: false
      })
    }
  },
    methods:{
      usercollection(){
       // axios.get("api/user").then(({data})=>(this.users=data));
        axios.get("api/users").then(({ data }) => (this.users = data.data));

      },
      userCreate(){
          this.form.post('api/users');
      }
    },
        created() {
            this.usercollection();
        }
    }
</script>
