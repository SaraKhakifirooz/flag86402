<template>
        <!-- <InputText name="firstName" v-bind="firstNameModel" /> -->
        <input v-bind="firstNameModel" class="bg-gray-200 mb-3" placeholder="name" />
        <span class="text-red-500">{{ errorMessage }}</span>

        <br>
        <input v-bind="lastNameModel" class="bg-gray-200 mb-3" placeholder="lastName" />
        <span class="text-red-500">{{ errorMessage }}</span>

        <!-- <InputText name="lastName" v-bind="lastNameModel" /> -->
        <br>
        <input v-bind="phoneModel" class="bg-gray-200 mb-3" placeholder="phoneModel" />
        <span class="text-red-500">{{ errorMessage }}</span>
        <!-- <InputText name="phone" v-bind="phoneModel" /> -->
        <br>
        <input v-bind="emailModel" class="bg-gray-200 mb-3" placeholder="emailModel" />
        <span class="text-red-500">{{ errorMessage }}</span>
        <!-- <InputText name="email" type="email" v-bind="emailModel" /> -->
        <br>
</template>
  
<script setup>
import { useForm } from 'vee-validate';
import * as yup from 'yup';

const phoneNumberValidation = /^((+98|0)?9\d{9})$/;


validationSchemaForm = yup.object({
    firstName: yup.string().required().min(11).max(256),
    lastName: yup.string().required().min(11).max(256),
    phone: yup.number().required().test((value, context) => {
        const customPhoneCondition = valid(value)
        return customPhoneCondition || context.createError({ message: "Please Enter a Correct Phone Number" })
    }),
    email: yup.string().required().email(),
});

const valid = (phone) => {
    console.log("phoneNumber ==>", phone)
    return phone.length && phone.test(phoneNumberValidation)
}

const { defineInputBinds, errors } = useForm({
    validationSchema: validationSchemaForm
})

const emailModel = defineInputBinds('emailSchema')
const firstNameModel = defineInputBinds('firstName')
const lastNameModel = defineInputBinds('lastName')
const phoneModel = defineInputBinds('phoneNumber')

</script>