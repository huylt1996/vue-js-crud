<template>
  <div class="crud">
    <h1>{{ msg }}</h1>
    <table class="table">
      <thead>
        <tr>
          <th scope="col" id="border-table-button">
            <!-- <button class="btn btn-primary" @click="handleAddItem">Add</button> -->
            <b-button v-b-modal.modal-prevent-closing @click="openDialog" style="background-color: #0d6efd !important; border-color: #0d6efd;">Add</b-button>
          </th>
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
    <!--Modal dialog add-->
    <div>
      <!-- <div class="mt-3">
        Submit Names:
        <div v-if="submittedNames.length === 0">--</div>
        <ul v-else class="mb-0 pl-3">
          <li v-for="(name,index) in submittedNames" :key="index">{{ name }}</li>
        </ul>
      </div> -->

      <b-modal
        id="modal-prevent-closing"
        ref="modal"
        title="Add new person"
        centered
        @show="resetModal" 
        @hidden="resetModal"
        @ok="handleOk"
        >

        <form ref="form" @submit.stop.prevent="handleSubmit">
          <b-form-group
            label="First Name"
            label-for="first-name-input"
            invalid-feedback="Name is required"
            :state="nameState">
              <b-form-input
                id="firstName"
                v-model="personDetail.firstName"
                :state="nameState"
                placeholder="Enter first name"
                required>
              </b-form-input>
          </b-form-group>
          <b-form-group
            label="Last Name"
            label-for="last-name-input"
            invalid-feedback="Name is required"
            :state="nameState">
              <b-form-input
                id="lastName"
                v-model="personDetail.lastName"
                :state="nameState"
                placeholder="Enter last name"
                required>
              </b-form-input>
          </b-form-group>
        </form>
      </b-modal>
    </div>
  </div>
</template>

<script>
// import Vue from "vue";
// import Modal from "../modals/compnents/Modal.vue";
// import ModalHeader from "../modals/compnents/ModalHeader.vue";
// import ModalFooter from "../modals/compnents/ModalFooter.vue";
// import ModalBody from "../modals/compnents/ModalBody.vue";
// // import ModalRoot from '../modals/compnents/ModalRoot.vue';
// import ModalMixin from "../modals/mixis/ModalMixin";
import ModalService from "../modals/services/modal.service";
import TestModal from "../components/TestModal.vue";

/* eslint-disable */
export default {
  // components: { Modal, ModalHeader, ModalFooter, ModalBody },
  // mixins: [ModalMixin],
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
      name: '',
      nameState: null,
      submittedNames: []
    };
  },
  created() {
    // debugger;
    this.listPerson = [
      { stt: 1, firstName: "Huy", lastName: "Lee" },
      { stt: 2, firstName: "Dao", lastName: "Lee" },
      { stt: 3, firstName: "Minh Anh", lastName: "Lee" },
      { stt: 4, firstName: "Hoang", lastName: "Lee" },
    ];
  },
  methods: {
    handleUpdate(index) {
      alert("Updating " + "record " + index);
      if(this.personDetail !== null){
        this.personDetail = [];
      }
      Object.assign(this.personDetail, this.listPerson[index]);
      this.indexUpdate = index;
      this.checkUpdate = true;
    },
    handleDelete(index) {
      alert("Deleting " + "record " + index);
      this.listPerson.splice(index, 1);
      for (let i = index; i < this.listPerson.length; i++) {
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
    handleAddItem() {
      alert("Add new item");
      ModalService.open(TestModal);
    },
    // addModal(){
    //   ModalService.open(this);
    // }
    checkFormValidity(){
      const valid = this.$refs.form.checkValidity()
      this.nameState = valid
      return valid
    },
    resetModal(){
      this.firstName = ''
      this.lastName= ''
      this.nameState = null
    },
    handleOk(bvModalEvt){
      // Prevent modal form closing
      bvModalEvt.preventDefault()
      this.handleSubmit()
    },
    handleSubmit(){
      // Exit when the form isn't valid
      if(!this.checkFormValidity()){
        return
      }
      // Push the name submitted names
      //this.submittedNames.push(this.name)
      let length = this.listPerson.length
      this.personDetail.stt = length + 1
      this.listPerson.push(this.personDetail)
      // Push the name to submitted names
      this.$nextTick(() => {
        this.$bvModal.hide('modal-prevent-closing')
      })
    },
    openDialog(){
      if(this.personDetail !== null){
        this.personDetail = [];
      }
    }
  },
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
