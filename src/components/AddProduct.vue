
<template>

  <div>
    <div id="Title">
    <h1 id="Logo">Grade-Memory</h1>
    <p>Enter new grades</p>
  </div>
    <div class="field">
      <label class="label">subject</label>
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
      <button class="button is-success" @click="saveProduct">SAVE</button>
    </div>
  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 
export default {
  created () {
  },
  name: "AddProduct",
  data() {
    return {
      subject: "",
      mark: "",
      weighting: "",
      comment: "",
      classaverage: "",
    };
  },
  methods: {
    // Create New product
    async saveProduct() {
      try {
        await axios.post("http://localhost:5000/products", {
          subject: this.subject,
          mark: this.mark,
          weighting: this.weighting,
          comment: this.comment,
          classaverage: this.classaverage,

        });
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