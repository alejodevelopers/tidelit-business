<script setup>
import { reactive, computed, ref } from "vue";
import { RouterLink, useRouter } from "vue-router";
import { useAuthStore } from "@/stores/auth.js";
const router = useRouter();
const auth = useAuthStore();

const credentials = ref({
  email: null,
  password: null,
});

const loginFn = async () => {
  try {
    await auth.login(credentials.value);
  } catch (error) {
    console.log(error.message);
  }
  await router.push("/");
};
const logoUrl = computed(() => {
  return `layout/images/${
    layoutConfig.darkTheme.value ? "logo-white" : "logo-dark"
  }.svg`;
});
</script>


<template>
  <div class="py-8">
    <div
      class="surface-ground flex align-items-center justify-content-center min-h-screen min-w-screen overflow-hidden"
    >
      <div class="flex flex-column align-items-center justify-content-center">
        <div
          style="
            border-radius: 56px;
            padding: 0.3rem;
            background: linear-gradient(
              180deg,
              var(--primary-color) 10%,
              rgba(33, 150, 243, 0) 30%
            );
          "
        >
          <div
            class="w-full surface-card py-8 px-5 sm:px-8"
            style="border-radius: 53px"
          >
            <div class="text-center mb-5">
              <img
                src="/img/logo-footer.png"
                alt="Image"
                width="300"
                class="mb-4"
              />
              <div class="text-900 text-3xl font-medium mb-3">Welcome</div>
              <span class="text-600 font-medium">Sign in to continue</span>
            </div>

            <div>
              <label for="email" class="block text-900 text-xl font-medium mb-2"
                >E-mail</label
              >
              <InputText
                id="email"
                type="email"
                placeholder="Email"
                class="w-full md:w-30rem mb-5"
                style="padding: 1rem"
                v-model.trim="credentials.email"
              />

              <label
                for="password"
                class="block text-900 font-medium text-xl mb-2"
                >Password</label
              >
              <InputText
                id="password"
                type="password"
                placeholder="Password"
                class="w-full md:w-30rem mb-5"
                style="padding: 1rem"
                v-model.trim="credentials.password"
              />

              <div
                class="flex align-items-center justify-content-between mb-5 gap-5"
              >
                <div class="flex align-items-center">
                  <Checkbox
                    v-model="checked"
                    id="rememberme1"
                    binary
                    class="mr-2"
                  ></Checkbox>
                  <label for="rememberme1">Remember me</label>
                </div>
                <a
                  class="font-medium no-underline ml-2 text-right cursor-pointer"
                  style="color: var(--primary-color)"
                  >Forgot password?</a
                >
              </div>
              <Button
                label="Sign In"
                class="w-full p-3 text-xl"
                @click="loginFn"
              ></Button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <AppConfig simple />
</template>

<style scoped>
.pi-eye {
  transform: scale(1.6);
  margin-right: 1rem;
}

.pi-eye-slash {
  transform: scale(1.6);
  margin-right: 1rem;
}
</style>
