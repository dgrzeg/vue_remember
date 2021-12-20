<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing.</p>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Unde odit
        dolores tenetur voluptas blanditiis quae repellendus nesciunt a vero
        minus!
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okey</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" v-model="title" />
      </div>
      <div class="form-control">
        <label for="title">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          v-model="description"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" id="link" name="link" v-model="link" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      inputIsInvalid: false,
      title: '',
      description: '',
      link: '',
    };
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      if (
        this.title.trim() === '' ||
        this.description.trim() === '' ||
        this.link.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(this.title, this.description, this.link);
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
