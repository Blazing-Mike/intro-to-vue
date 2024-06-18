<script setup>
import { ref } from 'vue';

const firstName = ref('');
const lastName = ref('');
const company = ref('');
const workEmail = ref('');
const companySize = ref('');
const fundingStage = ref('');
const message =  ref('');

const applicantEmail =  'adebambomich683@gmail.com';
const formEndpoint = 'https://eodh6njvzgfl22j.m.pipedream.net';

const handleSubmit = async (event) => {
  event.preventDefault(); // Prevent the default form submission

  const formData = {
    firstName: firstName.value,
    lastName: lastName.value,
    company: company.value,
    workEmail: workEmail.value,
    companySize: companySize.value,
    fundingStage: fundingStage.value,
    message: message.value,
    applicantEmail: applicantEmail,
  };

  try {
    const response = await fetch(formEndpoint, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(formData),
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
         <label for="firstName">First Name * : {{ firstName }}</label>
          <input type="text"  name="firstName" v-model="firstName" required />
      </div>

      <div class="form-group">
              <label for="lastName">Last Name *</label>
              <input type="text" id="lastName" name="lastName" v-model="lastName" required>
          </div>
          <div class="form-group">
              <label for="company">Company *</label>
              <input type="text" id="company" name="company" v-model="company" required>
          </div>
          <div class="form-group">
              <label for="workEmail">Work Email *</label>
              <input type="email" id="workEmail" name="workEmail" v-model="workEmail" required>
          </div>
          <div class="form-group">
              <label for="companySize">Company Size * :{{  companySize }}</label>
              <select id="companySize" name="companySize" v-model="companySize" required>
                  <option :value=" '0-10'">0-10 employees</option>
                  <option :value="'11-50'">11-50 employees</option>
                  <option :value="'51-100'">51-100 employees</option>
              </select>
          </div>
          <div class="form-group">
              <label for="fundingStage">Funding Stage : {{ fundingStage }}</label>
              <select id="fundingStage" name="fundingStage" v-model="fundingStage">
                  <option value="">Select funding stage</option>
                  <option value="under ₦100k">Under ₦100k</option>
                  <option value="₦100k - ₦500k">₦100k - ₦500k</option>
                  <option value="₦500k - ₦1m">₦500k - ₦1m</option>
              </select>
          </div>
          <div class="form-group">
              <label for="message">Any other Message : {{ message }}</label>
              <textarea id="message" name="message" v-model="message"></textarea>
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
