<template>
<div class="form-container">
    
<div class="page">
    <h4>Đăng nhập</h4>
    <ContactForm :contact="newContact" @submit:contact="createContact" />
    <p>{{ message }}</p>
    <p>Don't have an account? </p>
    <button class="btn btn-sm btn-success" @click="goToSigup">
<i class="fas fa-plus"></i> đăng ký
</button>
  </div>
</div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      newContact: {
        username: "",
        password: "",
      },
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        const check= await ContactService.checkLogIn(data);
        this.$router.push({ name: "contactbook" });
     }catch (error) {
        console.log(error);
        this.message = "Đăng nhập không thành công";
      }
    },
    goToSigup() {
this.$router.push({ name: "book.signup" });
},
  },
};
</script>