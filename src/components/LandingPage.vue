<template>
    <div>
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#">Basic ML Models</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav"
          aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link" @click="selectedModel = 'model1'" href="#">Model 1</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" @click="selectedModel = 'model2'" href="#">Model 2</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" @click="selectedModel = 'model3'" href="#">Model 3</a>
            </li>
          </ul>
        </div>
      </nav>
      <div class="container">
        <!-- Landing page content goes here -->

        <div v-if="selectedModel === 'model1'">
        <!-- Content for Model 1 -->
          <Model1Content />
        </div>
        <div v-else-if="selectedModel === 'model2'">
          <!-- Content for Model 2 -->
          <DynamicForm :schema="formSchema['fields']" :title="formSchema['title']" :subtitle="formSchema['subtitle']"/>
        </div>
        <div v-else-if="selectedModel === 'model3'">
          <!-- Content for Model 3 -->
          <DynamicForm :schema="formSchema2['fields']" :title="formSchema2['title']" :subtitle="formSchema2['subtitle']"/>
        </div>
        <div v-else>
          <!-- Default content when no model is selected -->
          <h2>Please select a model</h2>
        </div>
      </div>
    </div>
</template>
  
<script>
import Model1Content from './Model1Content.vue';
import DynamicForm from './DynamicForm.vue';

export default {
  components: {
    Model1Content,
    DynamicForm
  },
  data() {
    return {
      formSchema: {
        title: "Sign Up Form",
        subtitle: "",
        fields: {
          email: {
            label: 'Email',
            type: 'email',
          },
          password: {
            label: 'Password',
            type: 'password',
          },
          height: {
            label: 'Height (Inches)',
            type: 'number',
          },
          dob: {
            label: 'Date of Birth',
            type: 'date',
          },
          loa: {
            label: 'Letter of application',
            type: 'file',
          }
        }
      },
      formSchema2: {
        title: "Try our newest house price estimation model",
        subtitle: "Add house properties to estimate it's price",
        fields: {
          location: {
            label: 'Location',
            type: 'text',
          },
          doc: {
            label: 'Date of construction',
            type: 'date',
          }
        }
      },
      selectedModel: null
    };
  }
};
</script>
  
<style>
.navbar {
  background-color: #f8f9fa; /* Set the background color */
}

.navbar-brand {
  color: #333; /* Set the brand text color */
  font-weight: bold; /* Make the brand text bold */
}

.nav-link {
  color: #333; /* Set the link text color */
}

.nav-link:hover {
  color: #007bff; /* Change link color on hover */
}

.container {
  padding-top: 40px; /* Add top padding to the container */
}
</style>
  