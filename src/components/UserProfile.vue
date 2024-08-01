<template>
  <div class="container mt-5">
    <div class="card bg-dark bg-gradient text-white">
      <div class="card-header  text-center p-10">
        <h3>User Profile</h3>
      </div>
      <div class="card-body " style="background-color: rgb(141 149 150);">
        <div class="text-center mb-4">
          <div class="position-relative d-inline-block">
            <img @click="triggerFileInput" :src="profileImage" class="rounded-circle  profile-img" alt="Profile Image">
            <input type="file" ref="fileInput" @change="onImageChange" class="d-none">
          </div>
        </div>
        <form @submit.prevent="saveProfile" class="text-start" >
          <div class="row">
            <div class="col-md-6">
              <div class="form-group mb-3">
                <label for="firstName">First Name</label>
                <input 
                  type="text" 
                  v-model="user.firstName" 
                  class="form-control" 
                  id="firstName" 
                  :class="{'is-invalid': !validations.firstName}" 
                  required>
                <div v-if="!validations.firstName" class="invalid-feedback">
                  First name is required.
                </div>
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mb-3">
                <label for="lastName">Last Name</label>
                <input 
                  type="text" 
                  v-model="user.lastName" 
                  class="form-control" 
                  id="lastName" 
                  :class="{'is-invalid': !validations.lastName}" 
                  required>
                <div v-if="!validations.lastName" class="invalid-feedback">
                  Last name is required.
                </div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-md-6">
              <div class="form-group mb-3">
                <label for="email">Email</label>
                <input 
                  type="email" 
                  v-model="user.email" 
                  class="form-control" 
                  id="email" 
                  :class="{'is-invalid': !validations.email}" 
                  required>
                <div v-if="!validations.email" class="invalid-feedback">
                  Please enter a valid email address.
                </div>
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mb-3">
                <label for="phone">Phone Number</label>
                <input 
                  type="tel" 
                  v-model="user.phone" 
                  class="form-control" 
                  id="phone" 
                  :class="{'is-invalid': !validations.phone}" 
                  required>
                <div v-if="!validations.phone" class="invalid-feedback">
                  Phone number is required.
                </div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-md-6">
              <div class="form-group mb-3">
                <label for="nationality">Nationality</label>
                <input 
                  type="text" 
                  v-model="user.nationality" 
                  class="form-control" 
                  id="nationality" 
                  :class="{'is-invalid': !validations.nationality}" 
                  required>
                <div v-if="!validations.nationality" class="invalid-feedback">
                  Nationality is required.
                </div>
              </div>
            </div>
            <div class="col-md-6 ms-10">
              <div class="form-group mb-3">
                <label for="gender">Gender</label>
                <select 
                  v-model="user.gender" 
                  class="form-control" 
                  id="gender" 
                  :class="{'is-invalid': !validations.gender}" 
                  required>
                  <option value="">Select Gender</option>
                  <option value="Male">Male</option>
                  <option value="Female">Female</option>
                  <option value="Other">Other</option>
                </select>
                <div v-if="!validations.gender" class="invalid-feedback">
                  Gender is required.
                </div>
              </div>
            </div>
          </div>
          <div class="text-center mt-4">
            <button type="submit" class="btn btn-dark">Save Profile</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
        nationality: '',
        gender: ''
      },
      profileImage: 'https://thumbs.dreamstime.com/b/icono-del-perfil-del-placeholder-del-defecto-90197957.jpg',
      validations: {
        firstName: true,
        lastName: true,
        email: true,
        phone: true,
        nationality: true,
        gender: true
      }
    };
  },
  methods: {
    triggerFileInput() {
      this.$refs.fileInput.click();
    },
    onImageChange(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = e => {
          this.profileImage = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    },
    validateForm() {
      this.validations.firstName = !!this.user.firstName;
      this.validations.lastName = !!this.user.lastName;
      this.validations.email = /\S+@\S+\.\S+/.test(this.user.email);
      this.validations.phone = !!this.user.phone;
      this.validations.nationality = !!this.user.nationality;
      this.validations.gender = !!this.user.gender;
      return Object.values(this.validations).every(Boolean);
    },
    saveProfile() {
      if (this.validateForm()) {
        console.log('Profile saved:', this.user);
      } 
    }
  }
};
</script>

<style>

.container {
  max-width: 800px;
}
.card {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 0.5rem;
 
  padding: 10;
}
.profile-img {
  width: 250px;
  height:250px;
  cursor: pointer;
  border: rgb(51, 51, 126) solid 1px;
}
@media (max-width: 768px) {
  .profile-img {
    width: 200px;
    height: 200px;


  }
 
  .container {
    max-width: 80%;
    padding: 50px;
  
  }



  @media (max-width: 380px) {
  .profile-img {
    width: 100px;
    height: 100px;
  }

}

}
label{
  color:rgb(37, 26, 26);
  font-weight: bold;
}

</style>
