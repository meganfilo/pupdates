<template>
  <div class="home">
    <main>
      <h1>Schedule</h1>
      <section class="activity-log-wrapper">
        <ActivityLog :days="sortDates" />
      </section>
    </main>
    <AddActivityAside @grabFormData="addEvent" />
  </div>
</template>

<script>
// @ is an alias to /src
import AddActivityAside from "@/components/AddActivityAside.vue";
import ActivityLog from "@/components/ActivityLog.vue";

export default {
  name: "Home",
  components: {
    AddActivityAside,
    ActivityLog,
  },
  data() {
    return {
      days: [
        {
          date: "2021-07-06",
          events: [
            {
              id: "1",
              time: "7:00am",
              type: "Exercise",
              note: "2 mile walk",
            },
            {
              id: "2",
              time: "8:00am",
              type: "Food",
              note: "2 cups of kibble",
            },
          ],
        },
        {
          date: "2021-07-07",
          events: [
            {
              id: "1",
              time: "4:00am",
              type: "Bathroom",
              note: "Accident in the house!",
            },
            {
              id: "2",
              time: "8:00am",
              type: "Food",
              note: "2 cups of kibble",
            },
            {
              id: "3",
              time: "12:00pm",
              type: "Other",
              note: "Threw up",
            },
          ],
        },
        {
          date: "2021-08-07",
          events: [
            {
              id: "1",
              time: "4:00am",
              type: "Bathroom",
              note: "Accident in the house!",
            },
            {
              id: "2",
              time: "8:00am",
              type: "Food",
              note: "2 cups of kibble",
            },
            {
              id: "3",
              time: "12:00pm",
              type: "Other",
              note: "Threw up",
            },
          ],
        },
      ],
    };
  },
  computed: {
    sortDates() {
      let sorted = [...this.days];
      sorted.sort((dateA, dateB) => {
        // TODO: Revisit in the future - there must be a cleaner way of doing this.
        if (dateA.date.split("-")[0] == dateB.date.split("-")[0]) {
          // checks month
          if ((dateA.date.split("-")[1] = dateB.date.split("-")[1])) {
            // checks month
            if (dateA.date.split("-")[1] > dateB.date.split("-")[1]) {
              return -1;
            }
            // checks month
            if (dateA.date.split("-")[1] < dateB.date.split("-")[1]) {
              return 1;
            }

            // checks day
            if (dateA.date.split("-")[2] > dateB.date.split("-")[2]) {
              return -1;
            }
            // checks day
            if (dateA.date.split("-")[2] < dateB.date.split("-")[2]) {
              return 1;
            }
          }
        }
        if (dateA.date.split("-")[0] > dateB.date.split("-")[0]) {
          return -1;
        }
        if (dateA.date.split("-")[0] < dateB.date.split("-")[0]) {
          console.log(dateA.date, " is less than ", dateB.date);

          return 1;
        }
      });
      return sorted;
    },
  },
  methods: {
    addEvent(enteredDate, event) {
      const existingDateIndex = this.days.findIndex(
        (day) => day.date == enteredDate
      );

      if (existingDateIndex > 0) {
        this.days[existingDateIndex].events.push(event);
      } else {
        this.days.push({
          date: enteredDate,
          events: [{ ...event }],
        });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  min-height: 100vh;

  main {
    flex-grow: 1;
    padding-left: 1rem;
    padding-right: 1rem;
    padding-top: 3rem;
    max-width: 900px;
  }

  section {
    padding: 2rem 5rem;
  }
}
</style>
