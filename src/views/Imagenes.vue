<template>
  <div class="imagenes">
    <div class="container">
    <br>
    
      <div class="row">
        <div class="col">
          <br />
          <h2>Opciones de imagenes</h2>
          <br>
          <div class="form-group">
            <label for="exampleInputEmail1">Limite de imagenes</label>
            <input
              v-model="limite"
              type="number"
              class="form-control"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
            />
          </div>
          <div class="form-group">
            <label for="exampleInputPassword1">Pagina</label>
            <input
              v-model="page"
              type="number"
              class="form-control"
              id="exampleInputPassword1"
            />
          </div>
          <button @click="Buscar()" class="btn btn-primary">Buscar</button>
        </div>
        <div class="col-8">
        <b-carousel
      id="carousel-1"
      :interval="4000"
      controls
      indicators
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
      
    >
      <!-- Text slides with image -->
      <b-carousel-slide v-for="item in todos" :key="item.id"
        :text="item.author"
        :img-src="item.download_url"
      ></b-carousel-slide>
    </b-carousel>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// @ is an alias to /src
import axios from "axios";

export default {
  name: "Imagenes",
  data() {
    return {
      page: null,
      limite: null,
      todos: null,
    };
  },
  mounted() {
    this.page = 0;
    this.limite = 0;
    this.Buscar(this.page, this.limite);
  },
  methods: {
    Buscar() {
      if (this.page == 0) {
        this.page = this.random = Math.floor(Math.random() * (5 - 1 + 1)) + 1;
      } else {
        if (this.page < 0) {
          this.page = this.random = Math.floor(Math.random() * (5 - 1 + 1)) + 1;
        }
      }

      if (this.limite == 0) {
        this.limite = this.random = Math.floor(Math.random() * (5 - 1 + 1)) + 1;
      } else {
        if (this.limite < 0) {
          this.limite = this.random = Math.floor(Math.random() * (5 - 1 + 1)) + 1;
        }
      }
      this.getselect(this.page, this.limite);
    },
    getselect(page, limit) {
      axios
        .get("https://picsum.photos/v2/list?page=" + page + "&limit=" + limit)
        .then((Response) => {
          this.todos = Response.data;
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>
