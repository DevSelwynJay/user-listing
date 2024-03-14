<template>
  <q-page>
    <q-page-sticky position="top-right" :offset="[18, 18]">
        <div class="row items-center q-gutter-sm">
          <q-btn to="/admin" label="Go to Admin View" @click="linkClick" color="white" text-color="primary" />
        </div>
    </q-page-sticky>
    <RegistrationForm />
  </q-page>
</template>

<script setup>
  import RegistrationForm from 'components/RegistrationForm.vue'

  defineOptions({
    name: 'IndexPage'
  });
</script>
