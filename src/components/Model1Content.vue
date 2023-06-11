<template>
    <div>
      <div class="row">
        <div class="col-md-6">
          <!-- Image uploader section -->
          <h3>Image Uploader</h3>
          <div class="custom-file">
            <input type="file" class="custom-file-input" id="imageInput" @change="handleFileChange" accept="image/*" />
          </div>
          <div v-if="selectedImage">
            <!-- Display the selected image -->
            <img :src="selectedImage" alt="Selected Image" style="max-width: 100%; padding-top: 15px;" />
          </div>
          <div v-else>
            <p>No image selected.</p>
          </div>
          <button class="btn btn-primary mt-3" @click="processImage" :disabled="!selectedImage || processing">
            <span v-if="!processing">Process Image</span>
            <span v-else>
              <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
              Processing...
            </span>
          </button>
        </div>
        <div class="col-md-6">
          <!-- Result section -->
          <h3>Result</h3>
          <div v-if="processing">
            <p>Processing image...</p>
          </div>
          <div v-else-if="result">
            <!-- Display the result here -->
            <img :src="result" alt="Result Image" style="max-width: 100%" />
          </div>
          <div v-else>
            <p>No result available yet.</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>

  export default {
    data() {
      return {
        selectedImage: null,
        result: null,
        processing: false
      };
    },
    methods: {
        handleFileChange(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (e) => {
                const image = new Image();
                image.onload = () => {
                    const maxWidth = 300; // Maximum width for the image
                    const maxHeight = 300; // Maximum height for the image
                    let width = image.width;
                    let height = image.height;

                    if (width > maxWidth) {
                    height = (maxWidth / width) * height;
                    width = maxWidth;
                    }

                    if (height > maxHeight) {
                    width = (maxHeight / height) * width;
                    height = maxHeight;
                    }

                    // Create a temporary canvas to draw the resized image
                    const canvas = document.createElement('canvas');
                    const context = canvas.getContext('2d');
                    canvas.width = width;
                    canvas.height = height;
                    context.drawImage(image, 0, 0, width, height);

                    // Get the resized image as a data URL
                    const resizedImageUrl = canvas.toDataURL('image/jpeg');

                    // Set the selected image to the resized image
                    this.selectedImage = resizedImageUrl;
                };
                image.src = e.target.result;
                };
                reader.readAsDataURL(file);
            } else {
                this.selectedImage = null;
            }
        },
        processImage() {
            // Set the processing flag to true
            this.processing = true;
    
            // Perform the image processing asynchronously
            setTimeout(() => {
            // Process the selected image and update the result
            // For this example, we set a placeholder result image URL
            this.result = 'https://via.placeholder.com/300';
    
            // Reset the processing flag after 2 seconds
            setTimeout(() => {
                this.processing = false;
            }, 2000);
            }, 0);
        },
      // Add other methods or component logic here
    },
    // Add other component options or lifecycle hooks here
  };
  </script>
  
  <style scoped>
  /* Component-specific styles go here */
  .row {
    margin-top: 20px;
  }
  .col-md-6 {
    border: 1px solid #ddd;
    padding: 10px;
  }
  </style>
  