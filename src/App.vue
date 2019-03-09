<template>
   <div class="container">
      <form>
         <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
               <h1>File a Complaint</h1>
               <hr>
               <div class="form-group">
                  <label for="email">Mail</label>
                  <input
                     type="text"
                     id="email"
                     class="form-control"
                     v-model.lazy="userData.mail">
               </div>
               <div class="form-group">
                  <label for="password">Password</label>
                  <input
                     type="password"
                     id="password"
                     class="form-control"
                     v-model.lazy="userData.password">
               </div>
               <div class="form-group">
                  <label for="age">Age</label>
                  <input
                     type="number"
                     id="age"
                     class="form-control"
                     v-model="userData.age">
               </div>
            </div>
         </div>
         <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 form-group">
               <label for="message">Message</label><br>
               <!-- Interpolation between <textarea>{{ test }}</textarea> doesn't work!-->
               <textarea
                  id="message"
                  rows="5"
                  class="form-control"
                  placeholder="Your message here ... "
                  v-model.lazy="message"></textarea>
            </div>
         </div>
         <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
               <div class="form-group">
                  <label for="sendmail">
                  <input
                     type="checkbox"
                     id="sendmail"
                     value="SendMail"
                     v-model="sendMail"> Send Mail
                  </label>
                  <label for="sendInfomail">
                  <input
                     type="checkbox"
                     id="sendInfomail"
                     value="SendInfoMail"
                     v-model="sendMail"> Send Infomail
                  </label>
               </div>
            </div>
         </div>
         <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 form-group">
               <label for="male">
               <input
                  type="radio"
                  id="male"
                  value="Male"
                  v-model="gender"> Male
               </label>
               <label for="female">
               <input
                  type="radio"
                  id="female"
                  value="Female"
                  v-model="gender"> Female
               </label>
            </div>
         </div>
         <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 from-group">
               <label for="priority">Priority</label>
               <select
                  id="priority"
                  class="form-control"
                  v-model="selectedPriority"
                  @click="getPriorityClass()">
                  <option v-for="priority in priorities" :key="priority" :selected="priority"> 
                    {{ priority }} 
                  </option>
               </select>
            </div>
         </div>
         <hr>
         <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
               <button
                  class="btn btn-primary"
                  @click.prevent="submited()"
                  >Submit!
               </button>
            </div>
         </div>
      </form>
      <hr>
      <div class="row" v-if="isSubmitted">
         <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <div class="panel panel-default">
               <div class="panel-heading">
                  <h4>Your Data</h4>
               </div>
               <div class="panel-body">
                  <p>Mail: <span class="label label-info">{{ userData.mail }}</span></p>
                  <p>Password: <span class="label label-info">{{ userData.password }}</span></p>
                  <p>Age: <span class="label label-info">{{ userData.age }}</span></p>
                  <p style="width:523.011px; width:fit-content;">Message: <span style="white-space:pre; width:fit-content;" class="label label-info">{{ message }}</span></p>
                  <p><strong>Send Mail?</strong></p>
                  <ul class="list-group">
                     <li class="list-group-item list-group-item-success" v-for="mailType in sendMail" :key="mailType">{{ mailType }} <i class=" text-right fas fa-check-square"></i></li>
                  </ul>
                  <p>Gender: <span class="label label-info">{{ gender }}</span> </p>
                  <p>Priority:<span class="label" :class="getPriorityClass()">{{ selectedPriority }}</span></p>
                  
               </div>
            </div>
         </div>
      </div>
   </div>
</template>
<script>
   export default {
     data() {
       return {
         userData: {
            mail: '',
            password: '',
            age: 25
         },
         message: '',
         sendMail: [],
         gender: 'Male',
         priorities: ['High', 'medium', 'low'],
         selectedPriority: 'High',
         isSubmitted: false
       }
     
     },
      methods: {
         getPriorityClass() {
              if(this.selectedPriority === 'High'){
                return 'label-danger'
              }
              else if(this.selectedPriority === 'Medium'){
                return 'label-info'
              }
              else{
                return 'label-warning'
              }
         },
         submited() {
           this.isSubmitted= true;
         }
       }
   }
</script>
<style>
li{
  margin: 4px;
  width: 25%;
}

</style>