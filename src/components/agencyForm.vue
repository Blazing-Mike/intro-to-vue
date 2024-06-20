<script setup>
import { ref } from 'vue';

const formEndpoint = 'https://eodh6njvzgfl22j.m.pipedream.net';

const formData = ref({
  firstName : '',
  lastName: '',
  company: '',
  workEmail: '',
  companySize: '',
  fundingStage: '',
  applicantEmail: 'adebambomich683@gmail.com',
});

// create a value called reset form and set all data to an empty object


const handleSubmit = async (event) => {
  event.preventDefault(); // Prevent the default form submission

  try {
    const response = await fetch(formEndpoint, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(formData.value),
    });

    if (!response.ok) {
      throw new Error('Network response was not ok');
    }

    const result = await response.json();
    console.log('Success:', result);
    // Optionally, you can clear the form fields or provide feedback to the user here
  } catch (error) {
    console.error('Error:', error);
  }
};


</script>

<template>
  <div class="container">
    <form action="" @submit="handleSubmit">

      <div class="form-group">
         <label for="firstName">First Name * : {{ formData.firstName }}</label>
          <input type="text"  name="firstName" v-model="formData.firstName" required />
      </div>

      <div class="form-group">
              <label for="lastName">Last Name *</label>
              <input type="text" id="lastName" name="lastName" v-model="formData.lastName" required>
          </div>
          <div class="form-group">
              <label for="company">Company *</label>
              <input type="text" id="company" name="company" v-model="formData.company" required>
          </div>
          <div class="form-group">
              <label for="workEmail">Work Email *</label>
              <input type="email" id="workEmail" name="workEmail" v-model="formData.workEmail" required>
          </div>
          <div class="form-group">
              <label for="companySize">Company Size * :{{  formData.companySize }}</label>
              <select id="companySize" name="companySize" v-model="formData.companySize" required>
                  <option :value=" '0-10'">0-10 employees</option>
                  <option :value="'11-50'">11-50 employees</option>
                  <option :value="'51-100'">51-100 employees</option>
              </select>
          </div>
          <div class="form-group">
              <label for="fundingStage">Funding Stage : {{ formData.fundingStage }}</label>
              <select id="fundingStage" name="fundingStage" v-model="formData.fundingStage">
                  <option value="">Select funding stage</option>
                  <option value="under ₦100k">Under ₦100k</option>
                  <option value="₦100k - ₦500k">₦100k - ₦500k</option>
                  <option value="₦500k - ₦1m">₦500k - ₦1m</option>
              </select>
          </div>
          <div class="form-group">
              <label for="message">Any other Message : {{ formData.message }}</label>
              <textarea id="message" name="message" v-model="formData.message"></textarea>
          </div>
          <button type="submit">Submit</button>

    </form>
  </div>
</template>


<style scoped>

input, select,
textarea {
  width: 100%;
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
}

.container{
  min-width: 20rem;
  margin: 2rem auto;
}

@media screen and (min-width: 768px) {
  .container {
    width: 30rem;
  }
  
}

.agency-form{
  margin: 2rem auto;
  width: 60%;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-weight: bold;
  margin: 5px 0;
}
</style>
