<template>
  <form @submit.prevent="handleSubmit"  >
    <h1 class="title">{{ title }}</h1>
    <h3 class='subtitle'>{{ subtitle }}</h3>
    <label>{{ zipCodeLabel }}</label>
    <input type="zipCode" v-model="zipCode" >
    <div v-if="zipCodeError" class="zipCodeError">{{zipCodeError}}</div>

    <label>{{ ageLabel }}</label>
    <select v-model="selectedAgeOption">
         <option v-for="ageOption in ageOptions" :key="ageOption.id">{{ ageOption }}</option>
        
    </select>
    <label>{{ coverageAmountLabel }}</label>
    <select v-model="selectedCoverageAmount">
      <option v-for="coverageAmount in coverageAmounts" :key="coverageAmount.id">{{ coverageAmount }}</option>
    </select>
    <label>{{ policyTypeLabel }}</label>
    <select v-model="selectedPolicyType">
      <option v-for="policyType in policyTypes" :key="policyType.id">{{ policyType }}</option>
    </select>
    
    <div class="submit_btn">
      <button>
        {{ butCTA }}
      </button>
    </div>
  </form>
</template>

<script>
export default {
  data(){
    return {
      zipCode:'',
      selectedPolicyType:'',
      selectedCoverageAmount:'',
      selectedAgeOption:'',
      zipCodeError:''
    }
  },
  props: {
    title: {
      type: String,
      require: true,
    },
    subtitle:{
      type: String,
      require: true
    },
    butCTA: {
      type: String,
      require: true
    },
    zipCodeLabel:{
      type:String,
      require: true
    },
    ageOptions:{
      type: Array,
      require: true
    },
    coverageAmounts:{
      type: Array,
      require: true
    },
    policyTypes:{
      type: Array,
      require: true
    },
    ageLabel:{
      type: String,
      require: true
    },
    policyTypeLabel:{
      type: String,
      require:true
    },
    coverageAmountLabel:{
      type: String,
      require: true
    },
  },
  methods: {
    handleSubmit() {
      this.zipCodeError = this.zipCode.length === 5 ? '' : 'Zip code must be 5 digits';
      if(!this.zipCodeError){
        console.log(this.zipCode);
        console.log(this.selectedAgeOption);
        console.log(this.selectedCoverageAmount);
        console.log(this.selectedPolicyType);
        this.zipCode = "";
        this.selectedAgeOption = '';
        this.selectedCoverageAmount = ""
        this.selectedPolicyType = "";
      }
    }
  }
}
</script>


<style>
  form {
    border-bottom: solid 5px #0157ff;
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px 10px 0px 0px;
  }
  .title{
    text-align: center;
    color: black;
    /* font-family: "CircularStd-Book",Arial,sans-serif;   */
    /* font-size: 18px; */
  }
  .subtitle{
    text-align: center;
    color: rgb(81, 82, 96);
    font-family: 'CircularStd-Book',Arial,sans-serif; 
    font-size: 18px;
    line-height: 28px;
    margin-bottom: 32px;
  }

  label {
    color: black;
    display: inline-block;
    margin: 25px 0 15px;
    /* text-transform: uppercase; */
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    /* border: none; */
  }
  button{
    width: 100%;
    background: #0157ff;
    border: 0;
    padding: 15px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 5px;
  }
  .submit_btn{
    text-align: center;
  }
  .zipCodeError{
    color: red;
    margin-top: 10px;
    font-size: 0.8rem;
    font-weight: bolder;
  }


</style>
