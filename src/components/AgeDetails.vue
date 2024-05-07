<template>
  <div class="age-content">
    <div class="age-group">
        <label class="age-input">{{ age.years || '- -' }}</label>
        <label class="age-text">years</label>
    </div>
    <div class="age-group">
        <label class="age-input">{{ age.months || '- -'}}</label>
        <label class="age-text">months</label>
    </div>
    <div class="age-group">
        <label class="age-input">{{ age.days || '- -' }}</label>
        <label class="age-text">days</label>
    </div>
  </div>
</template>

<script setup>
import "../style/agedetails.css";
import { defineProps, onMounted } from "vue";
import gsap from "gsap";

const props = defineProps({
    age: {
        type: Object
    }
});

onMounted(() => {
    // Animation
    gsap.fromTo(props.age.years, { opacity: 0, y:10, scaleY: 0 }, { opacity: 1, y: 0, scaleY: 1, duration: 1, delay: 0.6, ease: "power1.out"});

    gsap.fromTo(props.age.months, { opacity: 0, y:10, scaleY: 0 }, { opacity: 1, y: 0, scaleY: 1, duration: 1, delay: 0.4, ease: "power1.out"});

    gsap.fromTo(props.age.days, { opacity: 0, y:10, scaleY: 0}, { opacity: 1, y: 0, scaleY: 1, duration: 1, delay: 0.2, ease: "power1.out"});
});

</script>