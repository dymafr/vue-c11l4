<template>
  <input @blur="handleChange" v-model="usernameValue" type="text" />
  <p v-if="usernameError">{{ usernameError }}</p>

  <pre>
    {{ usernameValue }}
  </pre>
</template>

<script setup lang="ts">
import { useForm, useField } from 'vee-validate';
import { z } from 'zod';
import { toFormValidator } from '@vee-validate/zod';

const validationSchema = z.object({
  username: z
    .string()
    .min(3, { message: 'Le champ est trop court' })
    .max(10, { message: 'Le champ est trop long' }),
});

useForm({
  validationSchema: toFormValidator(validationSchema),
  initialValues: { username: 'Test' },
});

const {
  value: usernameValue,
  errorMessage: usernameError,
  handleChange,
} = useField('username', null, { validateOnValueUpdate: false });
</script>

<style scoped lang="scss"></style>
