<template>
  <form id="form">
    <div class="form-control">
      <label for="text" class="lbl" :class="{ 'lbl-error': (!dayInput && errors) || invalidDate }">Day</label>
      <input
        class="input-field"
        :class="{ 'error-input': (!dayInput && errors) || invalidDate }"
        type="text"
        id="day"
        v-model="dayInput"
        placeholder="DD"
      />
      <p class="error-text" v-if="(invalidDate && !dayInput) || (!invalidDate && !dayInput && dayError)">{{ dayError }}</p>    </div>
    <div class="form-control">
      <label for="text" class="lbl" :class="{ 'lbl-error': (!monthInput && errors) || invalidDate }">Month</label>
      <input
        class="input-field"
        :class="{ 'error-input': (!monthInput && errors) || invalidDate }"
        type="text"
        id="month"
        v-model="monthInput"
        placeholder="MM"
      />
      <p class="error-text" v-if="(invalidDate && !monthInput) || (!invalidDate && !monthInput && monthError)">{{ monthError }}</p>    
    </div>
    <div class="form-control">
      <label for="text" class="lbl" :class="{ 'lbl-error': !yearInput && errors || invalidDate }">Year</label>
      <input
        class="input-field"
        :class="{ 'error-input': (!yearInput && errors) || invalidDate }"
        type="text"
        id="year"
        v-model="yearInput"
        placeholder="YYYY"
      />
      <p class="error-text" v-if="(invalidDate && !yearInput) || (!invalidDate && !yearInput && yearError)">{{ yearError }}</p>    
    </div>
    <div class="button-group">
      <div class="hr-container">
        <hr class="solid" />
      </div>
      <button class="btn" @click.prevent="calculateAge">
        <svg xmlns="http://www.w3.org/2000/svg" width="46" height="44" viewBox="0 0 46 44">
          <g fill="none" stroke="#FFF" stroke-width="2">
            <path d="M1 22.019C8.333 21.686 23 25.616 23 44M23 44V0M45 22.019C37.667 21.686 23 25.616 23 44"/>
          </g>
        </svg>
      </button>
    </div>
    <div class="container">
      <AgeDetails :age="age" />
    </div>
  </form>
</template>

<script setup>
import "../style/inputform.css";
import AgeDetails from "./AgeDetails.vue";
import { ref } from 'vue';

// This stores the user inputs
const dayInput = ref("");
const monthInput = ref("");
const yearInput = ref("");

// This is for validation purposes
const dayError = ref("");
const monthError = ref("");
const yearError = ref("");
const errors = ref(false);
const invalidDate = ref(false);

const age = ref({
  years: 0,
  months: 0,
  days: 0
});

function calculateAge() {
  // Validate the form regardless of missing inputs
  validateForm();

  if (!dayInput.value || !monthInput.value || !yearInput.value) {
    // Exit the function if there are missing inputs
    return;
  }

  // This stores the date in the format of YYYY-MM-DD
  const dobString = `${yearInput.value}-${monthInput.value}-${dayInput.value}`;

  console.log(dobString);

  const today = new Date();
  const date = new Date(dobString);

  // This gets the date value by splitting the date
  var dateOfBirth = date.toISOString().split('T')[0];

  var isDateValid = validateDate(dateOfBirth);

  if(!isDateValid) {
    dayError.value = "Invalid Date of Birth";
    monthError.value = "Invalid Date of Birth";
    yearError.value = "Invalid Date of Birth";
    invalidDate.value = true;

    return;
  }

  console.log(dateOfBirth);

  // This assigns the extracted year, month, and day to a number variable
  var year = parseInt(dateOfBirth.substr(0, 4));
  var month = parseInt(dateOfBirth.substr(4, 2));
  var day = parseInt(dateOfBirth.substr(6, 2));

  let yearsDiff = today.getFullYear() - year;
  let monthsDiff = today.getMonth() - month;
  let daysDiff = today.getDate() - day;
  
  if(monthsDiff < 0 || (monthsDiff === 0 && today.getDate() < dateOfBirth.getDate())) {
    yearsDiff--;
    monthsDiff += 12;
  }

  if(daysDiff < 0) {
    monthsDiff--;
    const prevMonth = new Date(today.getFullYear(), today.getMonth() - 1, today.getDate());
    daysDiff = Math.floor((today - prevMonth) / (1000 * 60 * 60 * 24));
  }
            
  age.value = {
    years: yearsDiff,
    months: monthsDiff,
    days: daysDiff
  };

  dayInput.value = "";
  monthInput.value = "";
  yearInput.value = "";
  errors.value = false;
  invalidDate.value = false;
}

function validateForm() {
  dayError.value = !dayInput.value ? "this field is required" : "";
  monthError.value = !monthInput.value ? "this field is required" : "";
  yearError.value = !yearInput.value ? "this field is required" : "";
  errors.value = true;
}

function validateDate(date) {
  date = String(date);

  // Format: YYYY-MM-DD
  var datePattern = /^([12]\d{3}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01]))/;

  // Check if the date string format is a match
  var matchArray = date.match(datePattern);

  if (matchArray == null) {
    return false;
  }

  // Remove any non digit characters
  var dateString = date.replace(/\D/g, ''); 

  // This assigns the extracted year, month, and day to a variable
  var year = parseInt(dateString.substr(0, 4));
  var month = parseInt(dateString.substr(4, 2));
  var day = parseInt(dateString.substr(6, 2));

  // Create a list of days of a month
  var daysInMonths = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
  
  if(year % 400 == 0 || (year % 100 != 0 && year % 4 == 0)) {
    daysInMonths[1] = 29;
  }

  if(month < 1 || month > 12 || day < 1 || day > daysInMonths[month - 1]) {
    return false;
  }

  return true;
}
</script>