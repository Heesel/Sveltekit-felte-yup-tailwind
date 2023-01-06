<script>
  import { validator } from "@felte/validator-yup";
  import { createForm } from "felte";
  import * as yup from "yup";

  const schema = yup.object({
      email: yup.string().email().required(),
      password: yup.string().required(),
  });

  const { form, errors } = createForm({
    onSubmit: async (values) => {
      const user = await schema.validate(values);
      console.log(user)
    },
  });
</script>

<div class="flex flex-col items-center justify-center w-screen h-screen bg-gray-200 text-gray-700">
  <h1 class="font-bold text-2xl">Tailwind svelte validation</h1>
  <form use:form action="#" method="post" class="flex flex-col bg-white rounded shadow-lg p-12 mt-12">
      <label class="font-semibold text-xs" for="email">Email</label>
      <input class="flex items-center h-12 px-4 w-64 bg-gray-200 mt-2 rounded focus:outline-none focus:ring-2" name="email" type="email" />
      <label class="font-semibold text-xs mt-3" for="password">Password</label>
      <input class="flex items-center h-12 px-4 w-64 bg-gray-200 mt-2 rounded focus:outline-none focus:ring-2" name="password" type="password" />
      <button class="flex items-center justify-center h-12 px-6 w-64 bg-blue-600 mt-8 rounded font-semibold text-sm text-blue-100 hover:bg-blue-700">Login</button>
      <div class="flex mt-6 justify-center text-xs">
          <a class="text-blue-400 hover:text-blue-500" href="#">Forgot Password</a>
          <span class="mx-2 text-gray-300">/</span>
          <a class="text-blue-400 hover:text-blue-500" href="#">Sign Up</a>
      </div>
  </form>
</div>
