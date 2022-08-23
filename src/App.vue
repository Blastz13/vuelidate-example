<template>
  <form v-on:submit.prevent>
    <p>$model</p>
    <input
        id="name"
        v-model="v$.name.$model"
    />
    <p>{{ v$.name.$errors }}</p>

    <p>@blur</p>
    <input
        id="desc"
        v-model.trim="desc"
        @blur="v$.desc.$touch()"
    />

    <p>{{ v$.desc.$errors }}</p>

    <p>onInput</p>
    <input
        id="desc2"
        v-model.trim="desc2"
        @input="v$.desc2.$touch()"
    />
    <input type="submit" @click="sub">
    <p>{{ v$.desc2.$errors }}</p>


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
      desc: '',
      desc2: ''
    }
  },
  methods: {
    sub(){
      this.v$.$validate()
      console.log(this.v$.errors);

      // if(this.v$.error){
      //   return false;
      // } else {
      //   ;
      // }
    }
  },
  validations () {
    return {
      name: { required, minLength: minLength(6) }, // Matches this.firstNam
      desc: { required, minLength: minLength(10) }, // Matches this.firstNam
      desc2: { required, minLength: minLength(10) }, // Matches this.firstNam
    }
  }
}
</script>