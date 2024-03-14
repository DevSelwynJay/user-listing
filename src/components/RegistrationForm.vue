<template>
    <section class="form-section">
        <form @submit.prevent="simulateSubmit" class="form">
            <div class="text-h4 q-pb-md">Registration</div>
            <div class="q-pb-md text-h6" v-if="submitted"><q-icon color="secondary" name="check" /> Account Created Successfully.</div>
            <div class="form-row">
                <q-input :disable="submitting" :error="firstNameValidation" outlined v-model="firstName" label="First Name" maxlength="100" pattern="[A-Za-z0-9\s]+" />
                <q-input :disable="submitting" :error="lastNameValidation" outlined v-model="lastName" label="Last Name" maxlength="100" pattern="[A-Za-z0-9\s]+" />
                <q-input :disable="submitting" :error="mobileNumberValidation" outlined v-model="mobileNumber" label="Mobile Number" maxlength="12" pattern="[A-Za-z0-9\s]+" />
                <q-input :disable="submitting" :error="dateValidation" outlined v-model="date" label="Date of Birth">
                    <template v-slot:prepend>
                    <q-icon name="event" class="cursor-pointer">
                        <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                        <q-date v-model="date">
                            <div class="row items-center justify-end">
                            <q-btn v-close-popup label="Close" color="primary" flat />
                            </div>
                        </q-date>
                        </q-popup-proxy>
                    </q-icon>
                    </template>
                </q-input>
                <q-input :disable="submitting" :error="addressValidation" outlined v-model="address" label="Address" maxlength="1000" />
                <div class="row justify-end">
                    <q-btn
                    type="submit"
                    :loading="submitting"
                    label="Submit"
                    color="primary"
                    padding="sm"
                    class="full-width"
                    >
                    <template v-slot:loading>
                        <q-spinner-facebook />
                    </template>
                    </q-btn>
                </div>
            </div>
        </form>
    </section>
</template>
  
<script setup>
    defineOptions({
        name: 'RegistrationForm'
    })

    import { ref } from 'vue'

    const firstName = ref('')
    const lastName = ref('')
    const mobileNumber = ref('')
    const date = ref('')
    const address = ref('')

    const submitting = ref(false)
    const submitted = ref('')
    const submissions = localStorage.getItem('submissions') ? ref(JSON.parse(localStorage.getItem('submissions'))) : ref([])

    const firstNameValidation = ref(false)
    const lastNameValidation = ref(false)
    const mobileNumberValidation = ref(false)
    const dateValidation = ref(false)
    const addressValidation = ref(false)

    function simulateSubmit () {
        firstNameValidation.value = firstName.value == "" ? true : false
        lastNameValidation.value = lastName.value == "" ? true : false
        mobileNumberValidation.value = mobileNumber.value == "" ? true : false
        dateValidation.value = date.value == "" ? true : false
        addressValidation.value = address.value == "" ? true : false
        if(firstName.value == "" || lastName.value == "" || mobileNumber.value == "" || date.value == "" || address.value == ""){
            return;
        }
        submitting.value = true
        saveFormDataToLocalStorage()
    }

    function saveFormDataToLocalStorage() {
      const formData = {
        firstName: firstName.value,
        lastName: lastName.value,
        mobileNumber: mobileNumber.value,
        date: date.value,
        address: address.value
      }
      submissions.value.push(formData);
      localStorage.setItem('submissions', JSON.stringify(submissions.value))
      setTimeout(() => {
        submitting.value = false
        submitted.value = true
        firstName.value = "";
        lastName.value = "";
        mobileNumber.value = "";
        date.value = "";
        address.value = "";
      }, 3000)
    }
</script>

  
<style lang="scss">
    .form-section{
        height: 100vh;
        width: 100%;
        display: grid;
        place-items: center;
        background: #4AC2D3;
        background: linear-gradient(135deg, #4AC2D3, #0367F4);
        padding: 1rem;
    }
    .form {
        background: #fff;
        max-width: 500px;
        width: 100%;
        box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
        padding: 2rem 2rem;
        border-radius: 8px;
    }
</style>