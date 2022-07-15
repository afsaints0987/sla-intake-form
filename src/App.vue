<template> 
<div>
  <div class="container w-75">
    <img src="../src/assets/wrike-logo-2.png" class="img-fluid" alt="wrike_logo" id="wrike-logo">
    <h1 class="text-center fw-bold my-4">Briefing Form</h1>
  </div>
  
    <!-- Project Container -->
    <form class="container-fluid" method='post' @submit.prevent> <!--Form to Submit -->
      <div class="container-fluid">
        <div class="container w-75">
          <div class="col">
            <!-- Brands -->
            <Header title="Brands" tooltip="Choose on different brands" />
            <select-field v-model="selected" :options="brands" label="Select Brands" required @customCheck="check" />
          </div>
        </div>
        <!-- Project Title || Project Task Title -->
        <div class="container w-75">
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
        
        <div class="container w-75">
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
          <div class="col">
            <Header title="What are our key messages?" />
            <input-field @customCheck="check" required/>
          </div>
        </div>
        <div class="container w-75">
          <div class="col">
            <text-field label="Which Consume (Delta) Segment are you targeting?" required/>
          </div>
          <div class="col">
            <text-field label="What 'need state' or Insight is this request delivering against?" required/>
          </div>
        </div>
          <!-- Parent Task  -->
        <div class="container w-75">
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
        <!-- Modal Form -->
        <modal label="Copy Requirements" id="copy" :options="assets"/>
        <modal label="Design Requirements" id="design" />
        <modal label="Motion Requirements" id="motion" />
        <modal label="Developer Requirements" id="dev" />

        <!-- Briefing Description -->
        <div class="container w-75">
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
    <Button class="btn btn-danger" text="Reset" @click="checkObject"/>
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
import RadioField from "./components/RadioField.vue";
import Modal from "./components/Modal.vue";
import { ref } from "vue";
export default {
  name: "App",
  props: {
    object: Object
  },
  data() {
    return {
      selected: "",
      checked: false,
      show: false
    };
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
      { id: 1, name: "All" },
      { id: 2, name: "New Customers" },
      { id: 3, name: "Existing Customers" },
      { id: 4, name: "Low Core" },
      { id: 5, name: "High Core" }
    ]);

    // Type of Task
    const tasks = ref([
      { id: 1, name: "Copy" },
      { id: 2, name: "Design" },
      { id: 3, name: "Motion" },
      { id: 4, name: "Developer" }
    ]);

    // Type of Priority
    const priority = ref([
      { id: 1, name: "Low" },
      { id: 2, name: "Medium" },
      { id: 3, name: "High" }
    ]);

    // Type of Campaign
    const campaign = ref([
      { id: 1, name: "New" },
      { id: 2, name: "Recurring" },
      { id: 3, name: "Promotion" }
    ]);
    // Assets
    const assets = ref([
      {
        id: 1,
        name: "Copy",
        content: [
          {
            name: "Promo Pack",
            asset: [
              { id: 1, value: "Banner Copy" },
              { id: 2, value: "Promo Hub" },
              { id: 3, value: "V6" },
              { id: 4, value: "Landing Page" },
              { id: 5, value: "Social Media" },
              { id: 6, value: "PAT Page" },
              { id: 7, value: "EDS" }
            ]
          },
          {
            name: "Treasure Chest",
            asset: [
              { id: 1, value: "Overlay" },
              { id: 2, value: "Inbox (CRM)" },
              { id: 3, value: "Toaster" },
              { id: 4, value: "SMS" },
              { id: 5, value: "Intro" },
              { id: 6, value: "Push (CRM)" },
              { id: 7, value: "Email (CRM)" },
              { id: 8, value: "Reminder Comms " }
            ]
          }
        ]
      },
      {
        id: 2,
        name: "Design",
        content: [
          {
            name: "Full Promo Pack",
            asset: [
              { name: "HT Mobile - L", value: "480x200" },
              { name: "HT Desktop - L", value: "1600x450" },
              { name: "Hp Slider", value: "1210x328" },
              { name: "Promo Page Background", value: "1210x328" },
              { name: "Promo Page Foreground", value: "605x328" },
              { name: "Promo Hub", value: "800x360" },
              { name: "Email Banner", value: "600x240" },
              { name: "Inbox Full View", value: "690x246" },
              { name: "Inbox Overlay", value: "420x123" },
              { name: "Inbox Preview", value: "66x65" },
              { name: "Desktop LP", value: "1920x938" },
              { name: "Tablet LP", value: "1024x1366" },
              { name: "Mobile LP", value: "828x1144" }
            ]
          },
          {
            name: "Gaming Static (Standard)",
            asset: [
              { name: "Instagram_Twitter_Facebook", value: "1080x1080" },
              { name: "Facebook_Profile", value: "180x180" },
              { name: "Facebook_RightHand", value: "255x133" },
              { name: "CRM", value: "335x280" },
              { name: "Snapchat", value: "360x600" },
              { name: "Twitter", value: "800x800" },
              { name: "Facebook_Cover", value: "851x315" },
              { name: "Carousel", value: "936x370" },
              { name: "Android_Push", value: "1038x600" },
              { name: "iOS_Push", value: "1038x800" },
              { name: "Instagram", value: "1080x1920" },
              { name: "Snapchat", value: "1080x1920" },
              { name: "Facebook", value: "1200x628" }
            ]
          },
          {
            name: "Sports Static (Standard)",
            asset: [
              { name: "1038x800_iOS_Push", value: "1038x800" },
              { name: "Android_Push", value: "1038x600" },
              { name: "CRM", value: "680x400" },
              { name: "CRM", value: "680x300" },
              { name: "Sub Feature", value: "330x348" },
              { name: "CRM", value: "335x280" },
              { name: "Carousel", value: "936x370" },
              { name: "Facebook", value: "1200x628" },
              { name: "Facebook_Post", value: "1200x900" },
              { name: "Facebook_Cover", value: "851x315" },
              { name: "Facebook_RightHand", value: "255x133" },
              { name: "Facebook_Profile", value: "180x180" },
              { name: "Snapchat", value: "360x600" },
              { name: "Instagram", value: "1080x1920" },
              { name: "Snapchat", value: "1080x1920" },
              { name: "Instagram_Twitter_Facebook", value: "1080x1080" }
            ]
          }
        ]
      },
      {
        id: 3,
        name: "Motion",
        content: [
          {
            id: 6,
            name: "Motion Asset",
            asset: [{ name: "Promo Banner" }, { name: "GIFs" }]
          }
        ]
      },
      {
        id: 4,
        name: "Developer",
        content: [
          {
            id: 7,
            name: "Developer Assets",
            asset: [
              { name: "Promo Pack" },
              { name: "Game Build" },
              { name: "Inbox / Treasure Chest" },
              { name: "Landing Page" }
            ]
          }
        ]
      }
    ]);

    return {
      brands,
      isChecked,
      tasks,
      priority,
      campaign,
      players,
      assets,
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
    RadioField,
    Modal
  },
  methods: {
    check(e) {
      console.log(e);
    },
    textFieldVal(e) {
      e.target.value == 1 ? this.show : !this.show;
    },
    checkObject() {
      console.log()
    }
  },
  created(){
    const assets = this.assets
    const asset = assets.map(asset => {
      return asset
    })
    const copy = asset[0]
    console.log(copy)
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
