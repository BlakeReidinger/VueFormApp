<template>
  <div class="submitted-ticket">
    <h3>Ticket Details: {{ ticket.category }}</h3>
    <p>Type: {{ ticket.type }}</p>
    <p>Subject: {{ ticket.subject }}</p>
    <p>Description: {{ ticket.description }}</p>
    <p>Ticket Files & Documents:</p>
    <ul>
      <li v-for="(file, index) in ticket.ticketFiles" :key="index">
        {{ file }}
      </li>
    </ul>
  </div>
</template>

<script>
import "./SubmittedTicket.css";
export default {
  name: "SubmittedTicket",
  props: {
    ticket: Object, // The submitted ticket data passed as a prop
  },
};
</script>

<style scoped>
/* Add your CSS styles for the submitted ticket component */
</style>
