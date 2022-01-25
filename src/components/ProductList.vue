
<template>


  <div>
  <div id="Title">
    <h1 id="Logo">Grade-Memory</h1>
    <p>All your grades at a glance</p>
  </div>
  
    <router-link :to="{ name: 'Create' }" class="button is-success mt-5"
      >Add New</router-link
    >
    <table class="table is-striped is-bordered mt-2 is-fullwidth table is-hoverable">
      <thead>
        <tr>
          <th>Subject</th>
          <th>Mark</th>
          <th>weighting</th>
          <th>comment</th>
          <th>class average</th>
          <th class="has-text-centered">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.exam_id">
          <td>{{ item.subject }}</td>
          <td>{{ item.mark }}</td>
          <td>{{ item.weighting }}</td>
          <td>{{ item.comment }}</td>
          <td>{{ item.classaverage }}</td>
          <td class="has-text-centered">
            <router-link
              :to="{ name: 'Edit', params: { id: item.exam_id } }"
              class="button is-info is-light"
              >Edit</router-link
            >
            <a
              class="button is-danger is-light"
              @click="deleteProduct(item.exam_id)"
              >Delete</a
            >
          </td>
        </tr>
      </tbody>
    </table>
<footer class="footer">
  <div class="content has-text-centered">
    <p>
      Programmed and designed by <strong>Tobias Binder & Yannis Eindiguer</strong>
    </p>
  </div>
</footer>

  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 
export default {
  name: "ProductList",
  data() {
    return {
      items: [],
    };
  },
 
  created() {
    this.getProducts();
  },
 
  methods: {
    // Get All Products
    async getProducts() {
      try {
        const response = await axios.get("http://localhost:5000/products");
        this.items = response.data;
      } catch (err) {
        console.log(err);
      }
    },
 
    // Delete Product
    async deleteProduct(id) {
      try {
        await axios.delete(`http://localhost:5000/products/${id}`);
        this.getProducts();
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
 
<style>
p{
  font-weight: 500;
  font-size: 20px;
}

#Title{
  height: 30px;
  width: 100%;
  text-align: center;
  margin: 300px 0 30px 0;
  

}

h1{
  font-weight: 500;
  font-size: 30px;
  color: #2B2D42;
}

.footer{
  background-color: #ffffff;
}


</style>