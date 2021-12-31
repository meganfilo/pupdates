<template>
  <div class="activity-item">
    <div class="item-info">
      <h4>
        <strong>{{ event.time }}</strong>
      </h4>
      <p v-if="event.type === 'Exercise'" aria-label="event.type">🦮</p>
      <p v-else-if="event.type === 'Food'" aria-label="event.type">🍖</p>
      <p v-else-if="event.type === 'Bathroom'" aria-label="event.type">💩</p>
      <p v-else aria-label="An event occured">❗</p>
    </div>
    <div class="item-note">
      <p>
        {{ event.note }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["event"],
};
</script>

<style lang="scss" scoped>
.activity-item {
  width: 100%;
  position: relative;
  padding: 1rem;
  border-bottom: 1px solid #fff;

  .item-info {
    display: flex;
    justify-content: space-between;
    align-items: center;

    p {
      font-size: 1.75em;
    }
  }

  .item-note {
    margin-top: 0.75rem;
    p {
      font-size: 1em;
      text-align: left;
    }
  }
}
</style>
