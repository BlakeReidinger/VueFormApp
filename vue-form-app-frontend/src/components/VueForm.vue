<template>
  <div class="ticket-details">
    <form @submit.prevent="submitForm" class="ticket-form">
      <h3 class="form-title">Ticket Details</h3>
      <div class="form-group">
        <div class="form-inline">
          <div class="form-group-inline">
            <!-- Category Dropdown -->
            <label for="category">Category:</label>
            <select
              v-model="category"
              @change="updateTypeOptions"
              class="select-category"
            >
              <option value="">Select Category:</option>
              <option value="Hardware">Hardware</option>
              <option value="Software">Software</option>
              <option value="Network">Network</option>
              <option value="In-Processing">In-Processing</option>
            </select>
          </div>
          <div class="form-group-inline">
            <!-- Type Input Field-->
            <label for="type">Type:</label>
            <select v-model="type" class="select-type">
              <!--v-for is used for rendering a list of items based on a arrays data.
              This will iterate over each item in the array and create a copy of a template for each item-->>
              <option v-for="option in typeOptions" :value="option">
                {{ option }}
              </option>
            </select>
          </div>
        </div>
      </div>
      <!-- Subject Input Field -->
      <div class="form-group">
        <label for="subject" class="subject-label">Subject:</label>
        <input type="text" v-model="subject" class="input-subject" />
      </div>
      <!-- Description Input Field -->
      <div class="form-group">
        <label for="description" class="description-label">Description:</label>
        <textarea v-model="description" class="textarea-description"></textarea>
      </div>
      <!-- Attach File Button -->
      <div class="form-group">
        <label for="ticketFiles" class="ticketFiles-label"
          >Ticket Files & Documents:</label
        >
        <button type="button" @click="attachFile" class="btn-attach-file">
          Attach File
        </button>
        <p v-for="(file, index) in ticketFiles" :key="index" class="file-info">
          {{ file }}
        </p>
      </div>
      <div class="form-button-group">
        <button type="button" @click="cancelForm" class="btn-cancel">
          Cancel
        </button>
        <button type="submit" class="btn-submit">Submit</button>
      </div>
    </form>
  </div>
  <hr />
  <!-- Display submitted tickets -->
  <div class="submitted-tickets">
    <SubmittedTicket
      v-for="(ticket, index) in submittedTickets"
      :key="index"
      :ticket="ticket"
    />
  </div>
</template>

<script>
import "./VueForm.css";
import SubmittedTicket from "./SubmittedTicket";

export default {
  name: "VueForm",
  components: {
    SubmittedTicket,
  },

  // Define the initial state of the component's data properties.
  // These properties are used to store various form data.
  data() {
    return {
      category: "", //Holds the category type
      type: "", // Holds the selected type
      subject: "", // Holds the subject entered by the user
      description: "", // Holds the description entered by the user
      ticketFiles: [], // Holds the list of files attached to the ticket
      submittedTickets: [], //Hold the list of tickets that were submitted
    };
  },

  //
  computed: {
    // Computed property to dynamically generate type options based on the selected category
    typeOptions() {
      //Type Options helps update the options available in the 'Type' dropdown menu for the selected category
      if (this.category === "Hardware") {
        return [
          "Laptop",
          "Mobile",
          "Peripherals",
          "Desk Phone",
          "Printers",
          "Other",
        ];
      } else if (this.category === "Software") {
        return [
          "Teams/Zoom",
          "Mobile Blackberry",
          "Adobe",
          "Outlook",
          "Microsoft Office",
          "Other",
        ];
      } else if (this.category === "Network") {
        return ["Network Access", "Connectivity", "VPN", "Drivers", "Other"];
      } else if (this.category === "In-Processing") {
        return ["Access Badge", "Common Access Card (CAC)", "SIPR", "Trello"];
      } else {
        return [];
      }
    },
  },
  methods: {
    // Method to update type options when category changes
    updateTypeOptions() {
      console.log("updateTypeOptions() called!");
      this.type = ""; // Reset selected type when category changes
      console.log("this.type = " + this.type);
    },
    // Method to add a file to the ticketFiles array
    attachFile() {
      console.log("attachFile() called!");
      const fileNumber = this.ticketFiles.length + 1; // Increment file number
      this.ticketFiles.push(`nameoffileattached${fileNumber}.ext`); // Add file to the list
    },
    // Method to handle form submission
    submitForm() {
      // Create a new ticket object with form data
      const newTicket = {
        category: this.category,
        type: this.type,
        subject: this.subject,
        description: this.description,
        ticketFiles: [...this.ticketFiles], // Copy of ticketFiles array
      };
      // Add the new ticket to the submittedTickets array
      this.submittedTickets.push(newTicket);
      // Clear the form
      this.cancelForm();
      console.log(this.submittedTickets);
    },
    // Method to handle cancel button click
    cancelForm() {
      this.category = "";
      this.type = "";
      this.subject = "";
      this.description = "";
      this.ticketFiles = [];
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #42b983;
}
</style>
