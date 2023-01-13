<script>
  import { createForm } from "felte";
  import * as yup from "yup";

  const schema = yup.object({
      email: yup.string().email('This field must be an email').required('This field is required'),
      password: yup.string().required('This field is required'),
  });

  const { form, errors } = createForm({
    validate: async (values) => {
      try {
        await schema.validate(values, { abortEarly: false });
      } catch(err) {
        
        const errors = err.inner.reduce((res, value) => ({
          [value.path]: value.message,
          ...res,
        }), {});
        
        return errors;
      }
    }
  });
</script>

<div class="flex flex-col items-center justify-center w-screen h-screen bg-gray-200 text-gray-700">
  <h1 class="font-bold text-2xl">Tailwind svelte validation</h1>
  
  <form use:form on:submit|preventDefault action="#" method="post" class="flex flex-col bg-white rounded shadow-lg p-12 mt-12">
      <label class="font-semibold text-xs" for="email">Email</label>
      <input class="flex items-center h-12 px-4 w-64 bg-gray-200 mt-2 rounded focus:outline-none focus:ring-2" name="email" type="email" />
      {#if $errors.email}
        <span class="text-red-500 text-sm">{$errors.email}</span>
      {/if}
      <label class="font-semibold text-xs mt-3" for="password">Password</label>
      <input class="flex items-center h-12 px-4 w-64 bg-gray-200 mt-2 rounded focus:outline-none focus:ring-2" name="password" type="password" />
      {#if $errors.password}
        <span class="text-red-500 text-sm">{$errors.password}</span>
      {/if}
      <button class="flex items-center justify-center h-12 px-6 w-64 bg-blue-600 mt-8 rounded font-semibold text-sm text-blue-100 hover:bg-blue-700">Login</button>
      <div class="flex mt-6 justify-center text-xs">
          <a class="text-blue-400 hover:text-blue-500" href="#">Forgot Password</a>
          <span class="mx-2 text-gray-300">/</span>
          <a class="text-blue-400 hover:text-blue-500" href="#">Sign Up</a>
      </div>
  </form>
</div>
