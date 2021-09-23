<template>
  <div class="setting-block">
    <div class="setting-title font-16 fw-500">Profile</div>

    <div class="setting-body white-bg-color">
      <form class="custom-form" @submit.prevent="update">
        <div class="row">
          <div class="col-md-6">
            
            <div class="alert alert-danger text-muted text-sm" v-if="form.successfully"  >
                Profile information updated successfully
            </div>
            <div class="form-group">
              <base-input :form="form" field="name" v-model="form.name" placeholder="Full name"></base-input>
            </div>
            <div class="form-group">
              <base-input :form="form" field="tagline" v-model="form.tagline" placeholder="Tagline"></base-input>
            </div>

            <div class="form-group">
              location
            </div>

            <div class="form-group">
              <base-textarea
                :form="form"
                field="about"
                :rows="4"
                v-model="form.about"
                placeholder="Please enter some information about yourself"
              ></base-textarea>
            </div>

            <div class="form-group custom-control custom-checkbox">
              <input
                type="checkbox"
                class="custom-control-input"
                id="available_to_hire"
                v-model="form.available_to_hire"
              />
              <label
                class="custom-control-label"
                :value="true"
                for="available_to_hire"
              >Available to hire?</label>
            </div>

            <div class="text-right">
              <base-button :loading="form.busy">Update profile</base-button>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: this.$vform({
        name: '',
        about: '',
        tagline: '',
        formatted_address: '',
        location: {},
        available_to_hire: false
      })
    };
  },
  methods: {
    update() {
      
    },
   
  },
  mounted() {
    console.log(JSON.stringify(this.$auth.user.data))
    Object.keys(this.form).forEach(k => {
      if (this.$auth.user.data.hasOwnProperty(k)) {
        this.form[k] = this.$auth.user.data[k];
      }
    });
    
    if (this.$auth.user.data.location) {
      this.form.location = {
        longitude: this.$auth.user.data.location.coordinates[0],
        latitude: this.$auth.user.data.location.coordinates[1]
      };
      
    } else {
      this.form.location = {};
    }
    console.log(JSON.stringify(this.form))
  }
};
</script>