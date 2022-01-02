<template>
  <aside>
    <h2>Add an activity</h2>
    <form @submit.prevent="submitForm">
      <div class="form-control">
        <label for="date-time"
          >Choose a date and time of your dog's event:</label
        >
        <input
          v-model="dateTime"
          type="datetime-local"
          id="date-time"
          name="meeting-time"
          min="2020-01-01T12:00"
          max="2022-12-31T00:00"
          required
        />
      </div>
      <div class="form-control">
        <p aria-label="Event type" id="eventType">Type of event:</p>
        <div role="radiogroup" aria-labelled-by="eventType">
          <input
            type="radio"
            id="exercise"
            name="exercise"
            value="exercise"
            v-model="type"
          />
          <label for="exercise" class="type-label"
            >Exercise <span class="type-icon">🦮</span></label
          >

          <input
            type="radio"
            id="meal"
            name="meal"
            value="meal"
            v-model="type"
          />
          <label for="meal" class="type-label"
            >Meal<span class="type-icon">🍖</span></label
          >

          <input
            type="radio"
            id="bathroom"
            name="bathroom"
            value="bathroom"
            v-model="type"
          />
          <label for="bathroom" class="type-label"
            >Bathroom<span class="type-icon">💩</span></label
          >

          <input
            type="radio"
            id="other"
            name="other"
            value="other"
            v-model="type"
          />
          <label for="other" class="type-label"
            >Other<span class="type-icon">❗</span></label
          >
        </div>
      </div>
      <div class="form-control" v-if="typeIsSelected">
        <label for="message">Additional Information:</label>
        <textarea
          id="message"
          name="message"
          v-model="message"
          rows="5"
          required
        ></textarea>
        <button type="submit">Log Event</button>
      </div>
    </form>
  </aside>
</template>

<script>
export default {
  emits: ["grabFormData"],
  data() {
    //2021-05-21T00:00
    return {
      eventId: Math.floor(Math.random() * 100),
      dateTime: new Date().toISOString().split("T")[0] + "T12:00",
      type: null,
      message: "",
      typeIsSelected: false,
      convertedDate: new Date().toISOString().split("T")[0],
      convertedTime: new Date().toISOString().split("T")[1],
    };
  },
  watch: {
    // if a type !== null, change typeIsSelected to true
    // this will show bottom half of form
    type: function () {
      this.typeIsSelected = true;
    },
    dateTime: function () {
      this.convertedDate = this.dateTime.split("T")[0];
      this.convertedTime = this.dateTime.split("T")[1];
    },
  },
  methods: {
    simplifyTime(militaryTime) {
      let hour = militaryTime.split(":")[0];
      let minutes = militaryTime.split(":")[1];
      let suffix;

      if (hour > 0 && hour < 12) {
        hour = hour.slice(1);
        suffix = "am";
      } else if (hour >= 12) {
        if (hour > 12) {
          hour = hour - 12;
        }
        suffix = "pm";
      } else if (hour == 0) {
        hour = 12;
        suffix = "am";
      }

      return hour + ":" + minutes + suffix;
    },
    resetForm() {
      this.eventId = Math.floor(Math.random() * 100);
      this.dateTime = new Date().toISOString().split("T")[0] + "T12:00";
      this.type = null;
      this.message = "";
      this.typeIsSelected = false;
      this.convertedDate = new Date().toISOString().split("T")[0];
      this.convertedTime = new Date().toISOString().split("T")[1];
    },
    submitForm() {
      console.log(this.dateTime);
      let date;
      let newEvent;
      if (
        this.type !== null &&
        this.dateTime !== "" &&
        this.message.trim() !== ""
      ) {
        date = this.convertedDate;
        newEvent = {
          id: this.eventId,
          time: this.simplifyTime(this.dateTime.split("T")[1]),
          type: this.type,
          note: this.message,
        };

        this.$emit("grabFormData", date, newEvent);
        this.resetForm();
      } else {
        // TODO: handle errors, add better UX
        console.log("enter more info");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
aside {
  width: 400px;
  max-height: 100vh;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  background-color: #42b983;
  padding-top: 3rem;
}

form {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-content: center;
  width: 100%;
  font-size: 1.15em;
  padding: 2rem;

  .form-control {
    text-align: left;
    margin: 0 auto;
    width: 100%;
  }

  p,
  label:not(.type-label) {
    display: block;
    font-size: 1em;
    font-weight: bold;
    margin-bottom: 1rem;
  }

  input[type="datetime-local"] {
    width: 100%;
    min-height: 3rem;
    font-size: 1em;
    padding: 1rem;
    font-family: "Avenir", sans-serif;
  }

  label.type-label {
    display: block;
    width: 100%;
    background: #fff;
    border: 1px solid transparent;
    border-radius: 10px;
    padding: 1rem;
    text-align: center;
    margin-bottom: 1rem;

    &:hover {
      border: 1px solid #2c3e50;
      cursor: pointer;
    }

    .type-icon {
      margin-left: 1rem;
    }
  }

  input[type="radio"] {
    display: none;
  }

  input[type="radio"]:checked + label.type-label {
    border: 1px solid #2c3e50;
    background: rgb(231, 230, 230);
  }

  div[role="radiogroup"] {
    margin-bottom: 2rem;
  }

  input,
  textarea {
    margin-bottom: 2rem;
  }

  textarea {
    display: block;
    min-width: 100%;
    min-height: 100px;
    padding: 0.5rem;
    font-size: 1em;
    font-family: "Avenir", sans-serif;
  }

  button {
    display: block;
    outline: none;
    border: none;
    padding: 1rem 2rem;
    background: #fff;
    color: #2c3e50;
    border-radius: 5px;
    font-size: 1em;
    font-weight: bold;
    text-align: center;

    &:hover {
      cursor: pointer;
      background: rgb(216, 214, 214);
    }
  }
}
</style>
