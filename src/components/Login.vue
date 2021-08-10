<template>
 <div id="main"  @submit="onSubmit"  >
    <b-form v-if="show"  >
      <b-form-group  class="marginBottom"
        id="input-group-1"
        label="User Name:"
        label-for="input-1"
  
      >
        <b-form-input
          id="input-1"
          v-model="form.UserName"
          placeholder="Enter User Name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Password:" label-for="input-2"  class="marginBottom">
        <b-form-input
          id="input-2"
          v-model="form.Password"
          placeholder="Enter Password"
          type="password"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="User Type:" label-for="input-3" class="marginBottom">
        <b-form-select
          id="input-3"
          v-model="form.UserType"
          :options="usertypes"
          required
        ></b-form-select>
      </b-form-group>
<!-- 
      <b-form-group id="input-group-4" v-slot="{ ariaDescribedby }"  class="marginBottom">
        <b-form-checkbox-group
          v-model="form.checked"
          id="checkboxes-4"
          :aria-describedby="ariaDescribedby"
        >
          <b-form-checkbox value="me">Check me out</b-form-checkbox>
          <b-form-checkbox value="that">Check that out</b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group> -->
<div>
  <b-button class="block" type="submit" variant="primary">Sing In</b-button>
</div>
   </b-form>
   <!-- <b-card class="mt-3 marginBottom" header="Form Data Result"  >
      <pre class="m-0">{{ form }}</pre>
    </b-card>-->
  </div> 
</template>

<script>
  export default {
  data() {
    return {
        form: {
           UserName: '',
          Password: '',
          UserType: 0,
        },
        data_message:[],
        usertypes: [{ text: 'Staff', value: 0 }, { text: 'Admin', value: 1 } ],
        show: true
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        this.$http.post('http://localhost:8003/API/Account/login',this.form).then(res=>
        { 
           this.$router.push('/Home')
        }).catch(function(err){
          if(err.response.status==404)
          {
            if(err.response.data.length>0)
            {
             alert( err.response.data[0].message);
            }
          }
          else if(err.response.status==400)
          {
               console.log(JSON.stringify( err.response.data.errors))
                // alert(err.response.data.errors.values);
          }
             
        })
          //if(res==null)  
             
         // });
       
      }
    }
  }
</script>
<style scoped>
#main {
  width:380px;
  height: 400px;
   text-align: left;
   float:right; 
   margin: 0px 300px;
 background-color: #e9ecef; 
padding: 40px;
}
#input-3{
  width: 100px;
  height: 26px;
}
.marginBottom{
  margin-bottom: 16px;
}
.block{
  display: block;
  width: 100%;
}
</style>



