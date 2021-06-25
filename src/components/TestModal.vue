<template>
  <Modal>
    <ModalHeader>
      <h3>Add Person</h3>
    </ModalHeader>
    <ModalBody>
      <p>Body of modal</p>
    </ModalBody>
    <ModalFooter>
      <button @click="close('Modal closed')" class="btn btn-primary">
        Close Modal
      </button>
      <button @click="dismiss('Modal dismissed')" class="btn btn-primary">
        Dismiss Modal
      </button>
    </ModalFooter>
  </Modal>
</template>

<script>
import Modal from "../modals/compnents/Modal.vue";
import ModalHeader from "../modals/compnents/ModalHeader.vue";
import ModalFooter from "../modals/compnents/ModalFooter.vue";
import ModalBody from "../modals/compnents/ModalBody.vue";
// import ModalRoot from '../modals/compnents/ModalRoot.vue';
import ModalMixin from "../modals/mixis/ModalMixin";
// import ModalService from "../modals/services/modal.service";
export default {
  components: { Modal, ModalHeader, ModalFooter, ModalBody },
  mixins: [ModalMixin],
};
</script>