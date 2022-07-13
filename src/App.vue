<template> 
<div>
  <div class="container w-50">
    <img src="../src/assets/wrike-logo-2.png" class="img-fluid" alt="wrike_logo" id="wrike-logo">
    <h1 class="text-center fw-bold my-4">Briefing Form</h1>
  </div>
  

    <!-- Project Container -->
    <form class="container-fluid" method='post' @submit.prevent> <!--Form to Submit -->
      <div class="container-fluid">
        <div class="container w-50">
          <div class="col">
            <!-- Brands -->
            <Header title="Brands" tooltip="Choose on different brands" />
            <select-field v-model="selected" :options="brands" label="name" placeholder="Select Brands" value="name" required @customCheck="check"/>
          </div>
        </div>
        <!-- Project Title || Project Task Title -->
        <div class="container w-50">
          <div class="col">
            <Header title="Project Title" tooltip="Please provide project title"/>
            <input-field @customCheck="check"/>
          </div>
          <!-- Requestor Name / Team || Briefing Description -->
          <div class="col" >
            <Header title="Requestor Name"/>
            <input-field @customCheck="check" />
          </div>
          <div class="col">
            <Header title="Requestor Team"/>
            <input-field @customCheck="check"/>
          </div>
        </div>
        
        <div class="container w-50">
          <!-- Briefing Description -->
          <div class="col">
            <Header title="Request / Campaign / Promotion Overview" tooltip="Please give us as much detail as possible to help inform out creative response. If it's a promotions, new or recurring, please add the mechanics here"/>
            <radio-field :fieldId="campaign.name" 
            :label="campaign.name" v-for="campaign in campaign" 
            :key="campaign"
            :name="campaign"
            :value="campaign.name"
            @radioCheck="check"/>
          </div>
          <div class="col">
            <Header title="Who are we talking to?"/>
            <radio-field :fieldId="player.name" 
            :label="player.name" v-for="player in players" 
            :key="player"
            :name="players"
            :checked="isChecked"
            :value="player.name"
            @radioCheck="check"
            />
            <div class="form-group">
              <input class="form-check-input" type="radio" id="player" :name="players" value="Others" v-model="checked" >
              <label class="form-check-label mx-2" for="player">Others</label>
              <input type="text" class="form-control-sm" value="" id="others" v-if="checked"  placeholder="Please specify customers">
            </div>
          </div>
        </div>
        
          <!-- Parent Task  -->
        <div class="container w-50">
          <div class="col">
            <Header title="Task Requirement"/>
            <checkbox-field :fieldId="task.name" 
            :label="task.name" v-for="task in tasks" 
            :key="task" 
            :checked="isChecked"
            :value="task.name"
            @checkValue="check"
            />
          </div>
        </div> 
        <!-- Briefing Description -->
        <div class="container w-50">
          <div class="col">
            <Header title="Campaign Planned Date Date" @checkDate="check"/>
            <date-field />
          </div>
          <!-- Finish Date -->
          <div class="col">
            <Header title="Desired Delivery Date"/>
            <date-field />
          </div>
        </div>
      </div>   
    </form>
    <div class="d-flex justify-content-center mt-4">
    <Button class="btn btn-danger" text="Reset"/>
    <Button class="btn btn-success" text="Submit" disabled/>
    </div>
</div>
</template>

<script>
import Header from "./components/Header.vue";
import InputField from "./components/InputField.vue";
import CheckboxField from "./components/CheckboxField.vue";
import DateField from "./components/DateField.vue";
import Button from "./components/Button.vue";
import SelectField from "./components/SelectField.vue";
import TextField from "./components/TextField.vue";
import RadioField from "./components/RadioField.vue"
import { ref } from "vue";
export default {
  name: "App",
  data(){
    return {
      selected: "",
      checked: false
    }
  },
  setup() {
    const isChecked = ref(false);
    // Brand List
    const brands = ref([
      { id: 1, name: "Cheeky Bingo" },
      { id: 2, name: "Coral Sports" },
      { id: 3, name: "Coral Gaming" },
      { id: 4, name: "Coral Retail" },
      { id: 5, name: "Foxy Bingo" },
      { id: 6, name: "Foxy Games" },
      { id: 7, name: "Gala Bingo" },
      { id: 8, name: "Gala Casino" },
      { id: 9, name: "Gala Spins" },
      { id: 10, name: "Ladbrokes Sports" },
      { id: 11, name: "Ladbrokes Gaming" },
      { id: 12, name: "Ladbrokes Retail" }
    ]);
    // Type of Players
    const players = ref([
      {id: 1, name: 'All'},
      {id: 2, name: 'New Customers'},
      {id: 3, name: 'Returning Customers'},
      {id: 4, name: 'VIP Customers'},
    ])

    // Type of Task
    const tasks = ref([
      { id: 1, name: "Copy" },
      { id: 2, name: "Design" },
      { id: 3, name: "Motion" },
      { id: 4, name: "Developer" }
    ]);

    // Type of Priority
    const priority = ref([
      {id: 1, name: 'Low'},
      {id: 2, name: 'Medium'},
      {id: 3, name: 'High'},
    ])

    // Type of Campaign
    const campaign = ref([
      {id: 1, name: 'New'},
      {id: 2, name: 'Recurring'},
      {id: 3, name: 'Promotion'}
    ])
    return {
      brands,
      isChecked,
      tasks,
      priority,
      campaign,
      players
    };
  },
  components: {
    Header,
    InputField,
    CheckboxField,
    DateField,
    Button,
    SelectField,
    TextField,
    RadioField
  },
  methods: {
    check(e){
      console.log(e)
    },
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:ital,wght@0,400;1,700&display=swap");
#app {
  font-family: $font;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  box-sizing: border-box;
}

</style>
