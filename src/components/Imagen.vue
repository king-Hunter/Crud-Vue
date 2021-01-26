<template>
  <div class="hello">
    <br />
    <div class="container">
      <br />
      <div class="row">
        <div class="col">
          <br />
          <h2>Opciones de imagen</h2>
          <br />
          <div class="form-group">
            <label for="exampleInputPassword1">ID</label>
            <input
              v-model="id"
              type="number"
              class="form-control"
              id="exampleInputPassword1"
            />
          </div>

          <div class="form-group">
            <label for="exampleInputEmail1">Filtros</label>
            <div class="input-group-prepend">
            </div>
            <b-form-select
              v-model="selected"
              :options="options"
            ></b-form-select>
            <br />
          </div>
          <div class="form-group">
            <label for="exampleInputEmail1">Ancho</label>
            <input
              v-model="ancho"
              type="number"
              class="form-control"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
            />
          </div>

          <div class="form-group">
            <label for="exampleInputPassword1">Alto</label>
            <input
              v-model="alto"
              type="number"
              class="form-control"
              id="exampleInputPassword1"
            />
          </div>
          <button @click="Buscar()" class="btn btn-primary">Buscar</button>
        </div>
        <div class="col-8">
          <div>
            <b-img :src="toda" fluid alt="Responsive image"></b-img>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Imagen",
  data() {
    return {
      url: null,
      selected: null,
      selected2: null,
      options: [
        { value: null, text: "Sleccione una opción" },
        { value: "blur", text: "Blur" },
        { value: "grayscale", text: "Grayscale" },
      ],
      alto: null,
      ancho: null,
      id: null,
      toda: null,
      validate: null,
    };
  },
  mounted() {
    this.alto = 0;
    this.ancho = 0;
    this.id = 0;
    this.Buscar();
  },
  methods: {
    Buscar() {
      if (this.alto == 0) {
        this.alto = 512;
      } else {
        if (this.alto < 0) {
          this.alto = 512;
        }
      }
      if (this.id == 0) {
        this.id = this.random = Math.floor(Math.random() * (100 - 1 + 1)) + 1;
      } else {
        if (this.id < 0) {
          this.id = this.random = Math.floor(Math.random() * (100 - 1 + 1)) + 1;
        }
      }

      if (this.ancho == 0) {
        this.ancho = 512;
      } else {
        if (this.ancho < 0) {
          this.ancho = 512;
        }
      }
      this.getselect(this.alto, this.ancho, this.id);
    },
    getselect(page, limit, id) {
      if (this.selected == null) {
        this.url = "https://picsum.photos/id/" + id + "/" + page + "/" + limit;
      } else {
        this.url =
          "https://picsum.photos/id/" +
          id +
          "/" +
          page +
          "/" +
          limit +
          "?" +
          this.selected;
      }
      axios
        .get(this.url)
        .then((Response) => {
          this.toda = Response.request.responseURL;
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
img.img-fluid {
    border-radius: 3%;
}
</style>
