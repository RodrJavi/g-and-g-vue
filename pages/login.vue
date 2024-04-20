<script lang="ts" setup>
const supabase = useSupabaseClient();
const email = ref("");
const password = ref("");
const passwordConfirm = ref("");
const isLoggingIn = ref(true);
const passwordsMatch = computed(() => {
  return password.value == passwordConfirm.value;
});
const checkEmail = ref(false);

const login = async () => {
  const { data, error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });

  if (!error) {
    navigateTo("/");
  }
};

const signUp = async () => {
  if (password.value.length > 4 && passwordsMatch) {
    const { data, error } = await supabase.auth.signUp({
      email: email.value,
      password: password.value,
    });

    password.value = "";
    email.value = "";
    passwordConfirm.value = "";

    if (data) {
      console.log(data);
    }
  }
};
</script>

<template>
  <div class="p-4">
    <p class="text-5xl py-4 text-center">Working out?</p>
    <p class="text-5xl py-4 text-center">Documenting food?</p>
    <p class="text-5xl py-4 text-center">Let's track those.</p>
    <div v-if="isLoggingIn">
      <form class="py-4" @submit.prevent="login()">
        <JInput
          label="Email"
          type="email"
          placeholder="email@email.com"
          v-model="email" />
        <JInput label="Password" type="password" v-model="password" />
        <button
          class="my-4 w-full border border-4 border-black rounded"
          type="submit">
          Log in
        </button>
      </form>
      <p class="text-center">
        New to us? That's cool.
        <u @click="() => (isLoggingIn = false)">Sign up</u>
      </p>
    </div>
    <div v-else>
      <form @submit.prevent="signUp()">
        <JInput
          label="Email"
          type="email"
          placeholder="email@email.com"
          v-model="email" />
        <JInput label="Password" type="password" v-model="password" />
        <JInput
          label="Confirm password"
          type="password"
          v-model="passwordConfirm" />
        <button
          class="my-4 w-full border border-4 border-black rounded"
          type="submit">
          Sign up
        </button>
      </form>
      <p class="py-4 text-center" v-if="checkEmail">
        check your email for confirmation!
      </p>
      <p class="text-center">
        Already have an account?
        <u @click="() => (isLoggingIn = true)">Log in</u>
      </p>
    </div>
  </div>
  {{ isLoggingIn }}
  {{ passwordsMatch }}
</template>
