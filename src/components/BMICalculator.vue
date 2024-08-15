<template>
  <div class="container mt-5 col-6">
    <h1 class="text-center">BMI Calculator</h1>
    <form @submit.prevent="calculateBMI">
      <div class="mb-3">
        <label for="weight" class="form-label">Weight (kg)</label>
        <input
          type="number"
          class="form-control"
          id="weight"
          v-model="weight"
          required
        />
      </div>
      <div class="mb-3">
        <label for="height" class="form-label">Height (cm)</label>
        <input
          type="number"
          class="form-control"
          id="height"
          v-model="height"
          required
        />
      </div>
      <button type="submit" class="btn btn-primary w-100">Calculate BMI</button>
    </form>
    <div v-if="bmi" class="mt-4 text-center">
      <h2>Your BMI: {{ bmi.toFixed(2) }}</h2>
      <p class="lead">{{ bmiCategory.category }}</p>
      <p>{{ bmiCategory.suggestion }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weight: null,
      height: null,
      bmi: null,
    };
  },
  computed: {
    bmiCategory() {
      if (this.bmi < 18.5) {
        return {
          category: "Underweight",
          suggestion:
            "Consider eating more nutritious foods and consult a healthcare provider for personalized advice.",
        };
      } else if (this.bmi >= 18.5 && this.bmi < 24.9) {
        return {
          category: "Normal weight",
          suggestion:
            "Maintain your current lifestyle and continue to eat a balanced diet and exercise regularly.",
        };
      } else if (this.bmi >= 25 && this.bmi < 29.9) {
        return {
          category: "Overweight",
          suggestion:
            "Consider incorporating more physical activity into your routine and monitor your diet to achieve a healthier weight.",
        };
      } else {
        return {
          category: "Obese",
          suggestion:
            "It’s important to consult a healthcare provider for personalized advice. Consider a balanced diet and regular exercise to improve your health.",
        };
      }
    },
  },
  methods: {
    calculateBMI() {
      const heightInMeters = this.height / 100;
      this.bmi = this.weight / (heightInMeters * heightInMeters);
    },
  },
};
</script>
