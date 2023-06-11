<template>
    <div class="dynamic-form">
        <h2>{{ title }}</h2>
        <p>{{ subtitle }}</p>

        <form @submit="handleSubmit" class="dynamic-form">
        <div v-for="(field, fieldName) in schema" :key="fieldName" class="mb-3">
            <label :for="fieldName" class="form-label">{{ field.label }}</label>
            <template v-if="field.type === 'file'">
            <input :type="field.type" :name="fieldName" class="form-control" @change="handleFileChange(fieldName)" />
            </template>
            <template v-else>
            <input :type="field.type" :name="fieldName" v-model="formValues[fieldName]" class="form-control" />
            </template>
        </div>

        <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>
</template>
  
<style scoped>
.dynamic-form {
    max-width: 400px;
    margin: 0 auto;
}
</style>
  

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    subtitle: {
      type: String,
      required: true,
    },
    schema: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      formValues: {}, // Object to store form field values
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      // Access the form field values in the `formValues` object and perform necessary actions
      console.log(this.formValues);
    },
    handleFileChange(fieldName) {
        const fileInput = event.target;
        const file = fileInput.files[0];
        this.formValues["File"] = file

        // You can perform additional operations with the selected file
        console.log(`Selected file for ${fieldName}:`, file);
    }
  },
};
</script>
