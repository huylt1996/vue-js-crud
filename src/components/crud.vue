<template>
  <div class="crud">
    <h1>{{ msg }}</h1>
    <table class="table">
      <thead>
        <tr>
          <th scope="col" id="border-table-button"><button class="btn btn-primary" @click="handleAddItem">Add</button></th>
        </tr>
        <tr>
          <th scope="col">#</th>
          <th scope="col">First Name</th>
          <th scope="col">Last Name</th>
          <th scope="col">Handle</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody
        v-for="(item, index) in listPerson"
        id="todo-list-example"
        ref="example"
        :key="index"
      >
        <tr>
          <th scope="row">{{ item.stt }}</th>
          <td>{{ item.firstName }}</td>
          <td>{{ item.lastName }}</td>
          <td></td>
          <td>
            <button
              type="button"
              class="btn btn-primary"
              @click="handleUpdate(index)"
            >
              Update
            </button>
            |
            <button
              type="button"
              class="btn btn-primary"
              @click="handleDelete(index)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <!--Process Update-->
    <div v-if="checkUpdate" style="margin-top: 100px">
      <form @submit.prevent="onSubmit">
        <div class="form-group">
          <label for="firstName">First Name</label>
          <input
            type="text"
            class="form-control"
            id="firstName"
            placeholder="Enter first name"
            v-model="personDetail.firstName"
          />
        </div>
        <div class="form-group">
          <label for="lastName">Last Name</label>
          <input
            type="text"
            class="form-control"
            id="lastName"
            placeholder="Enter last name"
            v-model="personDetail.lastName"
          />
        </div>
        <button class="btn btn-primary" @click="handleSubmitDataUpdate">
          Submit
        </button>
        |
        <button class="btn btn-primary" @click="cancel">Cancel</button>
      </form>
    </div>
  </div>
</template>

<script>
// import Vue from "vue";

/* eslint-disable */
export default {
  name: "crud",
  props: {
    msg: String,
    // ,
    // listPerson: Array
  },
  data() {
    return {
      listPerson: [],
      checkUpdate: false,
      personDetail: [],
      indexUpdate: -1,
    };
  },
  created() {
    // debugger;
    this.listPerson = [
      { stt: 1, firstName: "Huy", lastName: "Lee" },
      { stt: 2, firstName: "Dao", lastName: "Lee" },
      { stt: 3, firstName: "Minh Anh", lastName: "Lee" },
      { stt: 4, firstName: "Hoang", lastName: "Lee" }
    ];
  },
  methods: {
    handleUpdate(index) {
      alert("Updating " + "record " + index);
      Object.assign(this.personDetail, this.listPerson[index]);
      this.indexUpdate = index;
      this.checkUpdate = true;
    },
    handleDelete(index) {
      alert("Deleting " + "record " + index);
      this.listPerson.splice(index, 1);
      for(let i = index; i < this.listPerson.length; i++){
        this.listPerson[i].stt -= 1; 
      }
    },
    handleSubmitDataUpdate() {
      let length = this.listPerson.length;
      for (let i = 0; i < length; i++) {
        if (this.listPerson[i].stt - 1 === this.indexUpdate) {
          this.listPerson[i].firstName = this.personDetail.firstName;
          this.listPerson[i].lastName = this.personDetail.lastName;
          break;
        }
      }
      // this.$emit('on-update', this.listPerson);
      this.checkUpdate = false;
    },
    cancel() {
      this.checkUpdate = false;
      this.indexUpdate = -1;
    },
    handleAddItem(){
      alert("Add new item")
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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

#border-table-button {
  border-bottom-width: 0px !important;
}
</style>
