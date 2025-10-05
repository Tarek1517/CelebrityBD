<template>
  <div class="min-h-screen flex items-center justify-center p-4 py-20">
    <div class="w-full max-w-7xl">
      <!-- Modern Tab System -->
      <div class="flex justify-center mb-12">
        <div
          class="inline-flex bg-white/80 backdrop-blur-sm p-1.5 rounded-2xl shadow-lg border border-primary"
        >
          <button
            @click="activeTab = 'login'"
            :class="{
              'bg-gradient-to-r from-primary to-secondary text-white shadow-lg':
                activeTab === 'login',
              'text-primary hover:text-primary': activeTab !== 'login',
            }"
            class="py-3 px-8 font-semibold text-sm rounded-xl transition-all duration-300 cursor-pointer transform hover:scale-105"
          >
            Sign In
          </button>
          <button
            @click="activeTab = 'register'"
            :class="{
              'bg-gradient-to-r from-primary to-secondary text-white shadow-lg':
                activeTab === 'register',
              'text-primary hover:text-primary': activeTab !== 'register',
            }"
            class="py-3 px-8 font-semibold text-sm rounded-xl transition-all duration-300 cursor-pointer transform hover:scale-105"
          >
            Register
          </button>
        </div>
      </div>

      <!-- Tab Content -->
      <div
        class="bg-white/90 backdrop-blur-lg rounded-3xl shadow-2xl overflow-hidden border border-white/20"
      >
        <!-- Login Tab -->
        <div
          v-if="activeTab === 'login'"
          class="grid grid-cols-1 lg:grid-cols-2 min-h-[600px]"
        >
          <!-- Left Side - Form -->
          <div class="p-10 flex flex-col justify-center">
            <div class="max-w-xl mx-auto w-full">
              <div class="text-center mb-10">
                <div
                  class="inline-flex items-center justify-center w-16 h-16 bg-gradient-to-r from-primary to-secondary rounded-2xl shadow-lg mb-4"
                >
                  <Icon name="mdi:star" class="w-8 h-8 text-white" />
                </div>
                <h1
                  class="text-4xl font-bold bg-gradient-to-r from-gray-900 to-gray-700 bg-clip-text text-transparent mb-3"
                >
                  Welcome Back
                </h1>
                <p class="text-gray-600 text-lg">
                  Sign in to your celebrity account
                </p>
              </div>

              <form class="space-y-6">
                <div class="group">
                  <label
                    for="loginEmail"
                    class="block text-sm font-semibold text-gray-700 mb-3"
                  >
                    Email or Phone
                  </label>
                  <div class="relative">
                    <Icon
                      name="mdi:email"
                      class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
                    />
                    <input
                      id="loginEmail"
                      v-model="loginEmail"
                      type="text"
                      class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
                      placeholder="your@email.com or +8801XXXXXXXXX"
                    />
                  </div>
                </div>

                <div class="group">
                  <div class="flex justify-between items-center mb-3">
                    <label
                      for="loginPassword"
                      class="block text-sm font-semibold text-gray-700"
                    >
                      Password
                    </label>
                    <NuxtLink
                      to="/forget-password"
                      class="text-sm font-medium text-blue-600 hover:text-blue-800 transition-colors"
                    >
                      Forgot password?
                    </NuxtLink>
                  </div>
                  <div class="relative">
                    <Icon
                      name="mdi:lock-outline"
                      class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 group-focus-within:text-blue-600 transition-colors w-5 h-5"
                    />
                    <input
                      id="loginPassword"
                      v-model="loginPassword"
                      :type="showLoginPassword ? 'text' : 'password'"
                      class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
                      placeholder="••••••••"
                    />
                    <button
                      type="button"
                      @click="showLoginPassword = !showLoginPassword"
                      class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 hover:text-gray-600 transition-colors"
                    >
                      <Icon
                        :name="
                          showLoginPassword
                            ? 'mdi:eye-off-outline'
                            : 'mdi:eye-outline'
                        "
                        class="w-5 h-5"
                      />
                    </button>
                  </div>
                </div>

                <div class="flex items-center">
                  <input
                    id="remember"
                    v-model="rememberMe"
                    type="checkbox"
                    class="h-5 w-5 rounded border-gray-300 text-blue-600 focus:ring-blue-500 transition-colors"
                  />
                  <label
                    for="remember"
                    class="ml-3 block text-sm font-medium text-gray-700"
                  >
                    Remember me
                  </label>
                </div>
                <NuxtLink to="/Dashboard/index">
                  <button
                    type="submit"
                    class="w-full bg-gradient-to-r cursor-pointer from-primary to-secondary hover:from-secondary hover:to-primary text-white font-semibold py-4 px-6 rounded-xl transition-all duration-300 shadow-lg hover:shadow-xl transform hover:scale-105 flex items-center justify-center"
                  >
                    <span v-if="!loggingIn">Sign In</span>
                    <Icon
                      v-if="loggingIn"
                      name="mdi:loading"
                      class="animate-spin w-5 h-5 text-white"
                    />
                  </button>
                </NuxtLink>
              </form>

              <div class="mt-8">
                <div class="relative">
                  <div class="absolute inset-0 flex items-center">
                    <div class="w-full border-t border-gray-200"></div>
                  </div>
                  <div class="relative flex justify-center text-sm">
                    <span class="px-4 bg-white text-gray-500 font-medium"
                      >Or continue with</span
                    >
                  </div>
                </div>

                <div class="mt-6 grid grid-cols-2 gap-4">
                  <button
                    type="button"
                    @click="signInWithGoogle"
                    class="w-full inline-flex justify-center items-center py-3 px-4 border border-gray-200 rounded-xl shadow-sm bg-white text-sm font-medium text-gray-700 hover:bg-gray-50 transition-all duration-300 hover:shadow-md"
                  >
                    <Icon name="devicon:google" class="w-5 h-5" />
                    <span class="ml-2">Google</span>
                  </button>
                  <button
                    type="button"
                    @click="signInWithFacebook"
                    class="w-full inline-flex justify-center items-center py-3 px-4 border border-gray-200 rounded-xl shadow-sm bg-white text-sm font-medium text-gray-700 hover:bg-gray-50 transition-all duration-300 hover:shadow-md"
                  >
                    <Icon name="logos:facebook" class="w-5 h-5" />
                    <span class="ml-2">Facebook</span>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Right Side - Image -->
          <div class="hidden lg:block relative">
            <img
              src="/images/login.png"
              alt="Celebrity"
              class="w-full h-full object-cover"
            />
            <div
              class="absolute inset-0 bg-gradient-to-r from-primary/15 to-secondary/20"
            ></div>
          </div>
        </div>

        <!-- Register Tab -->
        <div
          v-if="activeTab === 'register'"
          class="grid grid-cols-1 lg:grid-cols-2 min-h-[600px]"
        >
          <!-- Left Side - Form -->
          <div class="p-10 flex flex-col justify-center">
            <div class="max-w-xl mx-auto w-full">
              <div class="text-center mb-10">
                <div
                  class="inline-flex items-center justify-center w-16 h-16 bg-gradient-to-r from-primary to-secondary rounded-2xl shadow-lg mb-4"
                >
                  <Icon name="mdi:account-plus" class="w-8 h-8 text-white" />
                </div>
                <h1
                  class="text-4xl font-bold bg-gradient-to-r from-gray-900 to-gray-700 bg-clip-text text-transparent mb-3"
                >
                  {{ isPhoneVerified ? "Complete Profile" : "Join Our Stars" }}
                </h1>
                <p class="text-gray-600 text-lg">
                  {{
                    isPhoneVerified
                      ? "Fill in your details to complete registration"
                      : "Create your celebrity account"
                  }}
                </p>
              </div>

              <form class="space-y-6">
                <!-- Phone Verification Step -->
                <div v-if="!isPhoneVerified" class="group">
                  <label class="block text-sm font-semibold text-gray-700 mb-3"
                    >Phone Number</label
                  >
                  <div class="flex gap-3">
                    <div class="relative w-1/3">
                      <button
                        type="button"
                        @click="showCountryDropdown = !showCountryDropdown"
                        class="w-full px-4 py-4 rounded-xl border border-gray-200 bg-white/50 backdrop-blur-sm flex items-center justify-between hover:bg-gray-50 transition-all duration-300"
                      >
                        <div class="flex items-center">
                          <img
                            :src="`https://flagcdn.com/w20/${selectedCountry.code.toLowerCase()}.png`"
                            class="w-5 h-3.5 mr-2 object-cover rounded"
                            :alt="selectedCountry.code"
                          />
                          <span class="text-sm font-medium">{{
                            selectedCountry.dialCode
                          }}</span>
                        </div>
                        <Icon
                          name="mdi:chevron-down"
                          class="h-4 w-4 ml-1 text-gray-500 transition-transform"
                          :class="{ 'rotate-180': showCountryDropdown }"
                        />
                      </button>

                      <div
                        v-if="showCountryDropdown"
                        class="absolute z-10 mt-2 w-full bg-white border border-gray-200 rounded-xl shadow-lg max-h-60 overflow-auto backdrop-blur-sm"
                      >
                        <div
                          v-for="country in countries"
                          :key="country.code"
                          @click="selectCountry(country)"
                          class="px-4 py-3 hover:bg-gray-50 cursor-pointer flex items-center transition-colors"
                        >
                          <img
                            :src="`https://flagcdn.com/w20/${country.code.toLowerCase()}.png`"
                            class="w-5 h-3.5 mr-3 object-cover rounded"
                            :alt="country.code"
                          />
                          <span class="text-sm font-medium">
                            {{ country.name }} ({{ country.dialCode }})
                          </span>
                        </div>
                      </div>
                    </div>

                    <input
                      v-model="phoneNumber"
                      type="tel"
                      class="flex-1 px-4 py-4 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white/50 backdrop-blur-sm transition-all duration-300 placeholder-gray-400"
                      placeholder="Phone number"
                    />
                  </div>
                </div>

                <!-- OTP Verification Field -->
                <div
                  v-if="showVerificationField && !isPhoneVerified"
                  class="group"
                >
                  <label
                    for="verificationCode"
                    class="block text-sm font-semibold text-gray-700 mb-3"
                    >Verification Code</label
                  >
                  <div class="flex gap-3">
                    <input
                      id="verificationCode"
                      v-model="verificationCode"
                      type="text"
                      class="flex-1 px-4 py-4 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white/50 backdrop-blur-sm transition-all duration-300 placeholder-gray-400"
                      placeholder="Enter 12345678"
                    />
                    <button
                      type="button"
                      @click="resendCode"
                      class="px-6 py-4 text-sm font-semibold bg-gradient-to-r from-blue-600 to-purple-600 hover:from-blue-700 hover:to-purple-700 cursor-pointer text-white transition-all duration-300 whitespace-nowrap rounded-xl shadow-lg hover:shadow-xl"
                    >
                      Resend
                    </button>
                  </div>
                  <p class="mt-2 text-xs text-gray-500">
                    Use <span class="font-bold text-blue-600">12345678</span> as
                    the verification code for testing
                  </p>
                </div>

                <!-- Registration Fields (shown after phone verification) -->
                <div v-if="isPhoneVerified" class="space-y-6">
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="group">
                      <label
                        for="firstName"
                        class="block text-sm font-semibold text-gray-700 mb-3"
                        >First Name</label
                      >
                      <input
                        id="firstName"
                        v-model="firstName"
                        type="text"
                        class="w-full px-4 py-4 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white/50 backdrop-blur-sm transition-all duration-300 placeholder-gray-400"
                        placeholder="John"
                      />
                    </div>
                    <div class="group">
                      <label
                        for="lastName"
                        class="block text-sm font-semibold text-gray-700 mb-3"
                        >Last Name</label
                      >
                      <input
                        id="lastName"
                        v-model="lastName"
                        type="text"
                        class="w-full px-4 py-4 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white/50 backdrop-blur-sm transition-all duration-300 placeholder-gray-400"
                        placeholder="Doe"
                      />
                    </div>
                  </div>

                  <div class="group">
                    <label
                      for="registerEmail"
                      class="block text-sm font-semibold text-gray-700 mb-3"
                      >Email</label
                    >
                    <div class="relative">
                      <Icon
                        name="mdi:email-outline"
                        class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 group-focus-within:text-blue-600 transition-colors w-5 h-5"
                      />
                      <input
                        id="registerEmail"
                        v-model="registerEmail"
                        type="email"
                        class="w-full pl-12 pr-4 py-4 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white/50 backdrop-blur-sm transition-all duration-300 placeholder-gray-400"
                        placeholder="your@email.com"
                      />
                    </div>
                  </div>

                  <div class="group">
                    <label
                      for="registerPassword"
                      class="block text-sm font-semibold text-gray-700 mb-3"
                      >Password</label
                    >
                    <div class="relative">
                      <Icon
                        name="mdi:lock-outline"
                        class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 group-focus-within:text-blue-600 transition-colors w-5 h-5"
                      />
                      <input
                        id="registerPassword"
                        v-model="registerPassword"
                        :type="showRegisterPassword ? 'text' : 'password'"
                        class="w-full pl-12 pr-12 py-4 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white/50 backdrop-blur-sm transition-all duration-300 placeholder-gray-400"
                        placeholder="••••••••"
                      />
                      <button
                        type="button"
                        @click="showRegisterPassword = !showRegisterPassword"
                        class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 hover:text-gray-600 transition-colors"
                      >
                        <Icon
                          :name="
                            showRegisterPassword
                              ? 'mdi:eye-off-outline'
                              : 'mdi:eye-outline'
                          "
                          class="w-5 h-5"
                        />
                      </button>
                    </div>
                    <p class="mt-2 text-xs text-gray-500">
                      At least 8 characters with a number and special character
                    </p>
                  </div>

                  <div class="group">
                    <label
                      for="confirmPassword"
                      class="block text-sm font-semibold text-gray-700 mb-3"
                      >Confirm Password</label
                    >
                    <div class="relative">
                      <Icon
                        name="mdi:lock-check-outline"
                        class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 group-focus-within:text-blue-600 transition-colors w-5 h-5"
                      />
                      <input
                        id="confirmPassword"
                        v-model="confirmPassword"
                        :type="showConfirmPassword ? 'text' : 'password'"
                        class="w-full pl-12 pr-12 py-4 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white/50 backdrop-blur-sm transition-all duration-300 placeholder-gray-400"
                        placeholder="••••••••"
                      />
                      <button
                        type="button"
                        @click="showConfirmPassword = !showConfirmPassword"
                        class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 hover:text-gray-600 transition-colors"
                      >
                        <Icon
                          :name="
                            showConfirmPassword
                              ? 'mdi:eye-off-outline'
                              : 'mdi:eye-outline'
                          "
                          class="w-5 h-5"
                        />
                      </button>
                    </div>
                  </div>

                  <div class="flex items-start">
                    <div class="flex items-center h-5">
                      <input
                        id="terms"
                        v-model="acceptTerms"
                        type="checkbox"
                        class="h-5 w-5 rounded border-gray-300 text-blue-600 focus:ring-blue-500 transition-colors"
                      />
                    </div>
                    <div class="ml-3 text-sm">
                      <label for="terms" class="font-medium text-gray-700">
                        I agree to the
                        <a
                          href="/terms"
                          class="text-blue-600 hover:text-blue-800 font-semibold transition-colors"
                          >Terms of Service</a
                        >
                        and
                        <a
                          href="/privacy"
                          class="text-blue-600 hover:text-blue-800 font-semibold transition-colors"
                          >Privacy Policy</a
                        >
                      </label>
                    </div>
                  </div>
                </div>

                <button
                  type="button"
                  @click="handleRegisterStep"
                  class="w-full bg-gradient-to-r from-primary to-secondary hover:from-secondary hover:to-primary text-white font-semibold py-4 px-6 rounded-xl transition-all duration-300 shadow-lg hover:shadow-xl transform hover:scale-105 flex items-center justify-center"
                >
                  <span v-if="!sendingCode && !registering">
                    {{
                      isPhoneVerified
                        ? "Complete Registration"
                        : showVerificationField
                        ? "Verify Phone"
                        : "Send Verification Code"
                    }}
                  </span>
                  <Icon
                    v-if="sendingCode || registering"
                    name="mdi:loading"
                    class="animate-spin w-5 h-5 text-white"
                  />
                </button>
              </form>

              <div class="mt-6 text-center text-sm text-gray-500">
                Already have an account?
                <button
                  @click="activeTab = 'login'"
                  class="text-primary hover:text-secondary font-semibold transition-colors ml-1"
                >
                  Sign in
                </button>
              </div>
            </div>
          </div>

          <!-- Right Side - Image -->
          <div class="hidden lg:block relative">
            <img
              src="/images/register.png"
              alt="Celebrity Registration"
              class="w-full h-full object-cover"
            />
            <div
              class="absolute inset-0 bg-gradient-to-r from-primary/15 to-secondary/15"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const activeTab = ref("login");

// Login form data
const loginEmail = ref("");
const loginPassword = ref("");
const rememberMe = ref(false);
const showLoginPassword = ref(false);
const loggingIn = ref(false);

// Register form data
const firstName = ref("");
const lastName = ref("");
const registerEmail = ref("");
const phoneNumber = ref("");
const registerPassword = ref("");
const confirmPassword = ref("");
const showRegisterPassword = ref(false);
const showConfirmPassword = ref(false);
const acceptTerms = ref(false);
const registering = ref(false);

// Phone verification
const showVerificationField = ref(false);
const verificationCode = ref("");
const sendingCode = ref(false);
const isPhoneVerified = ref(false);

// Country selection
const showCountryDropdown = ref(false);
const selectedCountry = ref({
  code: "BD",
  name: "Bangladesh",
  dialCode: "+880",
});

const countries = [
  { code: "BD", name: "Bangladesh", dialCode: "+880" },
  { code: "US", name: "United States", dialCode: "+1" },
  { code: "IN", name: "India", dialCode: "+91" },
  { code: "PK", name: "Pakistan", dialCode: "+92" },
  { code: "UK", name: "United Kingdom", dialCode: "+44" },
];

const selectCountry = (country) => {
  selectedCountry.value = country;
  showCountryDropdown.value = false;
};

const handleRegisterStep = () => {
  if (!isPhoneVerified.value) {
    if (!showVerificationField.value) {
      sendVerificationCode();
    } else {
      verifyCode();
    }
  } else {
    completeRegistration();
  }
};

const sendVerificationCode = () => {
  if (!phoneNumber.value) {
    alert("Please enter your phone number");
    return;
  }

  sendingCode.value = true;

  // Simulate API call
  setTimeout(() => {
    sendingCode.value = false;
    showVerificationField.value = true;
    alert(
      `Verification code sent to ${selectedCountry.value.dialCode}${phoneNumber.value}\n\nUse code: 12345678`
    );
  }, 1000);
};

const verifyCode = () => {
  if (verificationCode.value !== "12345678") {
    alert("Please enter the correct verification code (12345678)");
    return;
  }

  sendingCode.value = true;

  // Simulate verification
  setTimeout(() => {
    sendingCode.value = false;
    isPhoneVerified.value = true;
    showVerificationField.value = false;
  }, 1000);
};

const completeRegistration = () => {
  if (
    !firstName.value ||
    !lastName.value ||
    !registerEmail.value ||
    !registerPassword.value ||
    !confirmPassword.value
  ) {
    alert("Please fill in all fields");
    return;
  }

  if (registerPassword.value !== confirmPassword.value) {
    alert("Passwords don't match");
    return;
  }

  if (!acceptTerms.value) {
    alert("Please accept the terms and conditions");
    return;
  }

  registering.value = true;

  // Simulate registration
  setTimeout(() => {
    registering.value = false;
    alert("Account created successfully! You can now sign in.");
    activeTab.value = "login";
    resetRegisterForm();
  }, 1500);
};

const resendCode = () => {
  sendingCode.value = true;

  // Simulate resend
  setTimeout(() => {
    sendingCode.value = false;
    alert("New verification code sent (12345678)");
  }, 800);
};

const resetRegisterForm = () => {
  firstName.value = "";
  lastName.value = "";
  registerEmail.value = "";
  phoneNumber.value = "";
  registerPassword.value = "";
  confirmPassword.value = "";
  verificationCode.value = "";
  acceptTerms.value = false;
  showVerificationField.value = false;
  isPhoneVerified.value = false;
};

const signInWithGoogle = () => {
  alert("Sign in with Google clicked");
  // Implement Google auth logic
};

const signInWithFacebook = () => {
  alert("Sign in with Facebook clicked");
  // Implement Facebook auth logic
};
</script>

<style>
/* Smooth transitions for all interactive elements */
button,
input,
a,
select {
  transition: all 0.2s ease;
}

/* Animation for dropdown */
.dropdown-enter-active,
.dropdown-leave-active {
  transition: opacity 0.2s, transform 0.2s;
}
.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
