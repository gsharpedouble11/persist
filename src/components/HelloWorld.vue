<template>
  <div class="hello">
    <form>
      <label for="firstName">First Name</label>
      <input 
        type="text" 
        id="firstName"
        @input="updateForm('firstName', $event.target.value)"
        :value="form.firstName" />
    
      <label for="lastName">Last Name</label>
      <input 
        type="text" 
        id="lastName" 
        @input="updateForm('lastName', $event.target.value)"
        :value="form.lastName" />
    
      <label for="email">Email</label>
      <input 
        type="email" 
        id="email" 
        @input="updateForm('email', $event.target.value)"
        :value="form.email" />
    
      <label for="framework">Favorite Framework</label>
      <select id="framework" @change="updateForm('framework', $event.target.value)">
        <option value="vue" :selected="form.framework === 'vue'">Vue</option>
        <option value="stillvue" :selected="form.framework === 'stillvue'">Vue!</option>
        <option value="vuevuevue" :selected="form.framework === 'vuevuevue'">Vue :D</option>
        <option value="okfine" :selected="form.framework === 'okfine'">Other</option>
      </select>
    
      <label for="extras">Describe why you love Vue</label>
      <textarea 
        id="extras" 
        @input="updateForm('extras', $event.target.value)"
        :value="form.extras"
        rows="5"></textarea>
    
      <label>
        <input 
          type="checkbox" 
          :checked="form.spam"
          @change="updateForm('spam', $event.target.checked)" />
        I want all the spams
      </label>
    
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      form: {
        firstName: '',
        lastName: '',
        email: '',
        framework: 'vue',
        extras: '',
        spam: false
      }
    }
  },
  methods: {
    openStorage () {
      return JSON.parse(localStorage.getItem('form'))
    },
    saveStorage (form) {
      localStorage.setItem('form', JSON.stringify(form))
    },
    updateForm (input, value) {
      this.form[input] = value

      //extract stored form
      let storedForm = this.openStorage() 
      // if non exists, default to empty object
      if (!storedForm) storedForm = {}

      //store new value
      storedForm[input] = value
      //save changes into localStorage
      this.saveStorage(storedForm)
    }
  },
  created () {
    const storedForm = this.openStorage()
    if (storedForm) {
      this.form = {
        ...this.form,
        ...storedForm
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .hello {
    display: flex;
    justify-content: center;
  }
  form {
    display: flex;
    flex-direction: column;
    width: fit-content;
    align-items: center;
  }
  label, input {
    margin: .5rem auto;
  }
</style>
