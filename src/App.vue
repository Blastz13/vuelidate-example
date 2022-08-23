<template>
  <form v-on:submit.prevent>
    <input
        id="name"
        v-model.trim="name"
        @input="v$.name.$touch()"
    />
    <p>{{ v$.name.$errors }}</p>

    <input
        id="desc"
        v-model.trim="desc"
        @input="v$.desc.$touch()"
    />
    <input type="submit" @click="sub">
    <p>{{ v$.desc.$errors }}</p>


<!--    <div v-if="$v.name.$dirty">-->
<!--      <p class="error-message" v-if="!$v.name.required">-->
<!--        Email must not be empty.-->
<!--      </p>-->
<!--    </div>-->
  </form>
</template>

<script>
import useVuelidate from '@vuelidate/core'
import {minLength, required} from '@vuelidate/validators'

export default {
  setup () {
    return { v$: useVuelidate() }
  },
  data () {
    return {
      name: '',
      desc: ''
    }
  },
  methods: {
    sub(){
      this.v$.$validate()
      console.log(this.v$.errors);

      if(this.v$.error){
        return false;
      } else {
        ;
      }
    }
  },
  validations () {
    return {
      name: { required, minLength: minLength(6) }, // Matches this.firstNam
      desc: { required, minLength: minLength(10) }, // Matches this.firstNam
    }
  }
}
</script>