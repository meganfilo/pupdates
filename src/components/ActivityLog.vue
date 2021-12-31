<template>
  <div v-for="day in days" :key="day.date">
    <h3 class="activities-date">{{ day.date }}</h3>
    <article class="activities-list" :events="day.events">
      <ActivityLogItem
        v-for="event in day.events"
        :key="event.id"
        :event="event"
      />
    </article>
  </div>
</template>

<script>
import ActivityLogItem from "@/components/ActivityLogItem.vue";

export default {
  components: {
    ActivityLogItem,
  },
  props: {
    days: {
      type: Object,
      required: true,
    },
  },
  computed: {
    sortTimes() {
      // TODO: sort times
      return "hi";
    },
  },
};
</script>

<style lang="scss" scoped>
.activities-date {
  position: relative;
  width: 100%;
  display: block;
  text-align: left;
  font-size: 1.25em;

  &:after {
    content: "";
    position: absolute;
    top: 50%;
    left: 7.5rem;
    width: 15rem;
    height: 1px;
    background-color: #000;
    z-index: 1;
  }
}

.activities-list {
  border-radius: 5px;
  background: #e0dede;
  margin-top: 0.5rem;
  margin-bottom: 2.5rem;
  padding: 1rem 2rem;
}
</style>
