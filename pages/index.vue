<template>
  <div >
    <section >
      <h1>Home Page!</h1>
      <lifeWidget
      :title='widget.title'
      :subtitle="widget.subtitle"
      :zipCodeLabel='widget.zipCodeLabel'
      :ageLabel="widget.ageLabel"
      :ageOptions="widget.ageOptions"
      :coverageAmountLabel="widget.coverageAmountLabel"
      :coverageAmounts="widget.coverageAmounts"
      :policyTypeLabel="widget.policyTypeLabel"
      :policyTypes="widget.policyTypes"
      :butCTA="widget.butCTA"
      />
    </section>
    <script src="//app.storyblok.com/f/storyblok-v2-latest.js" type="text/javascript">
</script>
  </div>
</template> 
 
<script>



export default {

  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories', {
      version:'draft',
      starts_with: 'insurance-widget/'
    }).then(res => {
      console.log('Response:',res)
      const widget = res.data.stories.map(lw => {
        return {
          title: lw.content.Title,
          subtitle: lw.content.Subtitle,
          zipCodeLabel: lw.content.zipCodeLabel,
          zipCode: lw.content.zipCode,
          ageLabel: lw.content.ageLabel,
          ageOptions: lw.content.ageOptions,
          coverageAmountLabel: lw.content.coverageAmountLabel,
          coverageAmounts: lw.content.coverAmounts,
          policyTypeLabel: lw.content.policyTypeLabel,
          policyTypes: lw.content.policyTypes,
          butCTA: lw.content.butCTA, 
        }
      })
      
      return {
        
        widget: widget[0]
      }
    })
  },
}
</script>


<style>
  body{
    background: grey;
  }
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
