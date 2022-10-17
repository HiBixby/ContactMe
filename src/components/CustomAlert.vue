<template>
  <div class="alert-container w-full px-5 my-5">
    <div
      :class="{ hidden: !success }"
      class="bg-green-100 rounded-lg py-5 px-6 mb-3 text-base text-green-700 inline-flex items-center w-full"
      role="alert"
    >
      <svg
        aria-hidden="true"
        focusable="false"
        data-prefix="fas"
        data-icon="check-circle"
        class="w-4 h-4 mr-2 fill-current"
        role="img"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 512 512"
      >
        <path
          fill="currentColor"
          d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z"
        ></path>
      </svg>
      <div v-if="success">메세지 전송 성공!</div>
      <div v-else-if="failure">메세지 전송 실패!</div>
      <button v-on:click="dismissAlert" class="ml-auto">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="fill-current text-gray-700"
          viewBox="0 0 16 16"
          width="20"
          height="20"
        >
          <path
            fill-rule="evenodd"
            d="M3.72 3.72a.75.75 0 011.06 0L8 6.94l3.22-3.22a.75.75 0 111.06 1.06L9.06 8l3.22 3.22a.75.75 0 11-1.06 1.06L8 9.06l-3.22 3.22a.75.75 0 01-1.06-1.06L6.94 8 3.72 4.78a.75.75 0 010-1.06z"
          ></path>
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CustomAlert",
  props: {
    success: Boolean,
    failure: Boolean,
  },
  methods: {
    dismissAlert: function () {
      console.log("dismiss alert from component");
      this.$emit("dismissAlert");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
