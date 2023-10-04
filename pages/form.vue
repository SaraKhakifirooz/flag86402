<template>
    <InputText name="firstName" />
    <br>
    <InputText name="lastName" />
    <br>
    <InputText name="phone" />
    <br>
    <InputText name="email" type="email" />
    <br>
    <button @click="onSubmit">Submit</button>
</template>
  
<script setup>

import { useForm } from 'vee-validate';
import * as yup from 'yup';

const { handleSubmit } = useForm({
    validationSchema: yup.object({
        firstName: yup.string().required(),
        lastName: yup.string().required(),
        phone: yup.number().required(),
        email: yup.string().required().email(),
    }),
});


const onSubmit = handleSubmit(values => {
    alert(JSON.stringify(values, null, 2));
});


</script>