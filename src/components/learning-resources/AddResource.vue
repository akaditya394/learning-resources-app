<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>All inputs are mandatory cannot be empty</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="handleSubmit">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleRef" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          type="text"
          rows="3"
          ref="descRef"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkRef" />
      </div>
      <div><base-button type="submit">Add Resource</base-button></div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    handleSubmit() {
      const enteredTitle = this.$refs.titleRef.value;
      const enteredDescription = this.$refs.descRef.value;
      const enteredUrl = this.$refs.linkRef.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredUrl);
    },

    confirmError() {
      this.inputIsInvalid = false;
    },
  },
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
