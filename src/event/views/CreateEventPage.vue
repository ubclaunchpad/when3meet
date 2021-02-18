<template>
  <div class="container">
    <form class="main">
      <!-- Left Components -->
      <div class="main-left">
        <div class="date card">
          <h3 class="heading">Pick the date</h3>
          <EventDatePicker v-if="isSingleEvent" class="date-picker" />
          <EventDayPicker v-if="!isSingleEvent" />
          <AppToggleExternalText
            class="toggle"
            toggle-left-text="Single"
            toggle-right-text="Recurring"
            :default-state="false"
            @toggled="switchEventType"
          />
        </div>
      </div>

      <!-- Right Components -->
      <div class="main-right">
        <!-- Time  Card -->
        <div class="time card">
          <!-- Pick the time -->
          <section class="time-picker">
            <h3 class="heading">Pick the time</h3>
            <div class="time-input">
              Between <input type="number" required />
              <select name="dropdown">
                <option value="AM" selected>AM</option>
                <option value="PM">PM</option>
              </select>
              and
              <input type="number" required />
              <select name="dropdown">
                <option value="AM" selected>AM</option>
                <option value="PM">PM</option>
              </select>
            </div>
          </section>

          <!-- Timezone -->
          <section class="timezone">
            <h3 class="heading">Timezone</h3>
            <div class="timezone-input">
              <svg
                class="icon-location"
                width="13"
                height="20"
                viewBox="0 0 13 20"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M6.5444 9.5C5.94921 9.5 5.3784 9.23661 4.95754 8.76777C4.53668 8.29893 4.30024 7.66304 4.30024 7C4.30024 6.33696 4.53668 5.70107 4.95754 5.23223C5.3784 4.76339 5.94921 4.5 6.5444 4.5C7.13959 4.5 7.71041 4.76339 8.13127 5.23223C8.55213 5.70107 8.78857 6.33696 8.78857 7C8.78857 7.3283 8.73052 7.65339 8.61774 7.95671C8.50496 8.26002 8.33966 8.53562 8.13127 8.76777C7.92288 8.99991 7.67548 9.18406 7.40321 9.3097C7.13093 9.43534 6.83911 9.5 6.5444 9.5ZM6.5444 0C4.87787 0 3.2796 0.737498 2.10118 2.05025C0.922769 3.36301 0.260742 5.14348 0.260742 7C0.260742 12.25 6.5444 20 6.5444 20C6.5444 20 12.8281 12.25 12.8281 7C12.8281 5.14348 12.166 3.36301 10.9876 2.05025C9.80921 0.737498 8.21093 0 6.5444 0Z"
                  fill="rgba(2,15,34,1.0)"
                />
              </svg>
              <select class="timezone-select" name="dropdown">
                <option class="timezone-option" value="Default" selected>
                  America/Vancouver - PST</option
                >
                <option class="timezone-option" value="Default">
                  Option #2</option
                >
                <option class="timezone-option" value="Default">
                  Option #3</option
                >
                <option class="timezone-option" value="Default">
                  Option #4</option
                >
                <option class="timezone-option" value="Default">
                  Option #5</option
                >
              </select>
            </div>
          </section>
        </div>

        <!-- Event Card -->
        <div class="event card">
          <section class="event-input">
            <h3 class="heading">Event name</h3>
            <input type="text" required />
            <button
              v-if="isHidden"
              class="btn-add-desc"
              type="button"
              @click="isHidden = false"
            >
              Add a description
            </button>
          </section>
          <section v-if="!isHidden" class=" event-input">
            <h3 class="heading">Description</h3>
            <div class="input-container">
              <button class="btn-close" type="button" @click="isHidden = true">
                <svg
                  width="25"
                  height="25"
                  viewBox="0 0 25 25"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M18.75 6.25L6.25 18.75"
                    stroke="#375786"
                    stroke-width="1.33333"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                  <path
                    d="M6.25 6.25L18.75 18.75"
                    stroke="#375786"
                    stroke-width="1.33333"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                </svg>
              </button>
              <textarea />
            </div>
          </section>
          <AppButton
            :class="'btn-primary'"
            class="btn-create"
            content="Create Event"
            type="submit"
          />
        </div>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppButton from "@/common/AppButton.vue";
import AppToggleExternalText from "@/common/AppToggleExternalText.vue";
import EventDatePicker from "@/event/components/DatePicker.vue";
import EventDayPicker from "@/event/components/DayPicker.vue";

export default defineComponent({
  //TODO: Store data -> props?
  //TODO: POST to backend
  //TODO: Validate legal time
  //TODO: Validate empty space Event Name
  //TODO: Focus on textarea on btn-add-desc click
  //TODO: Support 24HR via auto changing AM/PM
  //TODO: Toggle EventDayPicker
  //TODO: Add EventDayPicker component
  //TODO: Add typescripts i.e., eventName & eventDetails to index.ts
  //TODO: Add responsive support
  //TODO: Styling per designs
  //TODO: Comment & clean up code
  //FIXME: Width size of btn-add-desc
  components: {
    AppButton,
    AppToggleExternalText,
    EventDatePicker,
    EventDayPicker
  },

  props: {
    timezone: {
      type: String,
      required: true,
      default: () => "PST - Vancouver time"
    }
  },

  data() {
    return {
      isHidden: true,
      isSingleEvent: true
    };
  },

  computed: {},

  methods: {
    switchEventType(toggleState: boolean) {
      this.isSingleEvent = toggleState;
    }
  }
});
</script>

<style scoped>
/*------------------------------------*\
  # GLOBAL
\*------------------------------------*/
.container {
  /* Applies also to DatePicker due to overlapping name */
  /* Same size as  in Event view */
  padding: 7.875rem 10rem;
}

/* Override Global Heading */
.heading {
  text-align: left;
  align-self: flex-start;
}

/* Card styling */
.card {
  background: #fff;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 5px;
  width: 557px;
  padding: 14px 30px 39px 30px;
}

/* Input boxes */
.time-input input,
.time-input select,
.timezone select,
.event-input input,
.event-input textarea {
  background: #fff;
  border: 1px solid rgba(237, 242, 245);
  /* box-sizing: border-box; */
  border-radius: 5px;
  padding: 0.4rem;
}

/*------------------------------------*\
  # MAIN COMPONENTS
\*------------------------------------*/

.main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.main-left,
.main-right {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  margin: 0.5rem;

  height: 578px;
}

/*------------------------------------*\
  # LEFT COMPONENT
\*------------------------------------*/

.date {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}

.date-picker {
  /* Removes styling from DatePicker on .container*/
  padding: 0;
  align-self: center; /*Might not be doing anything */
}

/*------------------------------------*\
  # RIGHT COMPONENT
\*------------------------------------*/

/* ========= Time ========= */

.time {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.time-input {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0.5rem 0 1.5rem 0;
}

.time-input input {
  text-align: center;
  width: 15%;
}

.timezone-input {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.timezone-input .icon-location {
  position: absolute;
  left: 0.5rem;
}

.timezone-input select {
  width: 100%;
  padding-left: 1.5rem;
}

/* ========= Event ========= */

.event {
  display: flex;
  flex-direction: column;
}

.event-input {
  display: flex;
  flex-direction: column;
  margin-bottom: 2rem;
}

.btn-add-desc {
  background: none;
  font-family: Open Sans;
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  /*line-height: 0%;*/
  letter-spacing: 1.25px;
  text-decoration-line: underline;
  color: rgba(157, 157, 157, 1);

  /* text-transform: uppercase; */
  text-align: left;
  margin: 0.5rem 0;
}

.btn-add-desc:hover {
  cursor: pointer;
  opacity: 0.3;
}

.event-input textarea {
  width: 100%;
  min-height: 3rem;
  resize: none;
}

.input-container {
  position: relative;
}

.btn-close {
  background: none;
  position: absolute;
  cursor: pointer;
  right: 1rem;
  top: 0.6rem;
}

.btn-close:hover {
  opacity: 0.3;
}

.btn-create {
  width: 100%;
  padding: 0.25rem; /* Reduced padding */
}
</style>