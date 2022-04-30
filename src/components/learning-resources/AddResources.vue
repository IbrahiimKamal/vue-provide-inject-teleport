<template>
  <base-dialog v-if="inputIsValid" title="invalid input" @close="closeDialog">
    <template #default>
      <p>Please enter a valid input.</p>
      <p>Please enter a valid input.</p>
    </template>
    <template #actions>
      <base-button @click="closeDialog" mode="flat"> Close </base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          ref="desInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" name="link" id="link" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseCard from '../UI/BaseCard.vue';
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';

export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsValid: false,
    };
  },
  methods: {
    onSubmit() {
      const title = this.$refs.titleInput.value;
      const description = this.$refs.desInput.value;
      const link = this.$refs.linkInput.value;

      if (
        title.trim() === '' ||
        description.trim() === '' ||
        link.trim() === ''
      ) {
        this.inputIsValid = true;
        return;
      }

      this.addResource(title, description, link);

      this.$refs.titleInput.value = '';
      this.$refs.desInput.value = '';
      this.$refs.linkInput.value = '';
    },

    closeDialog() {
      this.inputIsValid = false;
    },
  },

  components: { BaseButton, BaseCard, BaseDialog },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
