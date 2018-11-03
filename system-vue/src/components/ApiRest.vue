<template>
       <div id="apirest">
          <div class="container-fluid">
             <div class="row">
                <div class="col-sm-12">
                  <form @submit.prevent="leerAPI" class="form-group">
                      <label class="control-label">Quantidade de resultados</label>
                      <div class="input-group">
                        <input class="form-control" v-model="quantidadeResultados">
                        <span class="input-group-btn">
                          <button class="btn.btn-primary" type="submit">Mostrar</button>
                        </span>
                      </div>
                  </form>
                  <h1>Vues.JS + Axios</h1>
                  <table class="table table-hover table-striped">
                    <thead>
                      <tr>
                        <th>ID</th>
                        <th>Nome</th>
                        <th>Sobrenome</th>
                        <th>Imagem</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="usuario in usuarios">
                        <td>{{ usuario.id }}</td>
                        <td>{{ usuario.first_name }}</td>
                        <td>{{ usuario.last_name }}</td>
                        <td>
                          <img :src="usuario.avatar">
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>         
             </div>
          </div>
       </div>   
</template>

<script>
export default {
  name: 'ApiRest',
  data () {
    return {
      usuarios: [],
      quantidadeResultados: 5
    }
  },
  methods: {
    leerAPI(){
      axios.get('https://reqres.in/api/users', {
        params: {
          'per_page': this.quantidadeResultados
        }
      }).then(response => {
          //console.log(response)
          this.usuarios = response.data.data
      }).catch(e => {
          console.log(e)
      })
    }
  },
  created(){
    this.leerAPI()
  }
}
</script>
