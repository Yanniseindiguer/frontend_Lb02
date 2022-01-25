/* eslint-disable */
<template>
  <div>
  <div id="Title">
    <h1 id="Logo">Grade-Memory</h1>
    <p>Edit your grades</p>
  </div>
    <div class="field">
      <label class="label">Subject</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="Subject"
          v-model="subject"
        />
      </div>
    </div>
 
    <div class="field">
      <label class="label">mark</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="Mark"
          v-model="mark"
        />
      </div>
    </div>

        <div class="field">
      <label class="label">weighting</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="weighting"
          v-model="weighting"
        />
      </div>
    </div>

      <div class="field">
      <label class="label">comment</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="comment"
          v-model="comment"
        />
      </div>
    </div>

         <div class="field">
      <label class="label">classaverage</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="classaverage"
          v-model="classaverage"
        />
      </div>
    </div>

    <div class="control">
      <button class="button is-success" @click="updateProduct">UPDATE</button>
    </div>
  </div>
</template>
 
<script>

// import axios
import axios from "axios";
 
export default {
  watch: {
  },
  name: "EditProduct",
  data() {
    return {
      subject: "",
      mark: "",
      weighting: "",
      comment: "",
      classaverage: "",
    };
  },
  created: function () {
    this.getProductById();
  },
  methods: {
    // Get Product By Id
    async getProductById() {
      try {
        const response = await axios.get(
          `http://localhost:5000/products/${this.$route.params.id}`
        );
        this.subject = response.data.subject;
        this.mark = response.data.mark;
        this.weighting = response.data.weighting;
        this.comment = response.data.comment;
        this.classaverage = response.data.classaverage;

      } catch (err) {
        console.log(err);
      }
    },
 
    // Update product
    async updateProduct() {
      // var letters = /^[A-Za-z]+$/;
      // var numbers = [0-6];  
      // if(this.subject.value.match(letters) && this.mark.value.match(numbers))
      try {
        await axios.put(
          `http://localhost:5000/products/${this.$route.params.id}`,
          {
          subject: this.subject,
          mark: this.mark,
          weighting: this.weighting,
          comment: this.comment,
          classaverage: this.classaverage,
          }

        );
        this.subject="";
        this.mark = "";
        this.weighting = "";
        this.comment = "";
        this.classaverage = "";
        
        this.$router.push("/");
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
</style>
