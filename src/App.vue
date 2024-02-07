<template>
  <div class="container">
    <div class="left">
      <div class="left-list">
        <div class="filler">SP2024</div>
        <div class="days">
          <div class="day" v-for="(day, index) in schedule.days" :key="index">{{ day }}</div>
        </div>
      </div>
    </div>
    <div class="right">
      <div class="times">
        <div class="time" v-for="(time, index) in schedule.timeline" :key="index">{{ time }}</div>
      </div>
      <div class="grids">
        <div class="lines">
          <div class="grid-container" v-for="index in schedule.timeline.length" :key="index">
            <div :class="{ 'grid-horizontal': true, 'odd-time': index % 2 === 0 }" />
          </div>
        </div>
        <div class="horizontal-lines">
          <div class="horizontal-line" v-for="index in 5" :key="index" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      schedule: {
        timeline: [
          '08:00',
          '08:30',
          '09:00',
          '09:30',
          '10:00',
          '10:30',
          '11:00',
          '11:30',
          '12:00',
          '12:30',
          '01:00',
          '01:30',
          '02:00',
          '02:30',
          '03:00',
          '03:30',
          '04:00',
          '04:30',
          '05:00',
          '05:30',
          '06:00'
        ],
        days: ['SATURDAY', 'SUNDAY', 'MONDAY', 'TUESDAY', 'WEDNESDAY', 'THURSDAY']
      }
    }
  }
}
</script>

<style>
:root {
  --horizontal-gap: 1rem;
  --components-gap: 1rem;
}

.container {
  display: flex;
  justify-content: center;
  flex-direction: row;
  gap: var(--components-gap);
}

.right {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: auto;
  gap: var(--components-gap);
}

.grids {
  position: relative;
  display: flex;
  align-items: center;
  width: 100%;
  height: 100%;
  border: 2px solid #e2e2e2;
  border-radius: 10px;
}

.times {
  display: flex;
  flex-direction: row;
  width: 100%;
  justify-content: space-around;
  gap: var(--horizontal-gap);
  padding-inline: 2rem;
  height: 3rem;
  background-color: gray;
  border-radius: 10px;
  font-variant-numeric: tabular-nums;
}

.time {
  height: 3rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.lines {
  display: flex;
  height: 100%;
  width: 100%;
  padding-inline: 2rem;
  justify-content: space-around;
  gap: var(--horizontal-gap);
}

.left {
  display: flex;
  flex-direction: row;
}

.left-list {
  display: flex;
  width: 10rem;
  flex-direction: column;
  gap: var(--components-gap);
}

.day {
  height: 3rem;
  background-color: rgb(141, 141, 219);
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.day:first-child {
  border-radius: 10px 10px 0px 0px;
}

.day:last-child {
  border-radius: 0px 0px 10px 10px;
}

.filler {
  height: 3rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  background-color: antiquewhite;
}

.time:nth-child(even) {
  color: red;
  font-size: 12px;
}

.grid-container {
  background: red;
  height: 100%;
}

.grid-horizontal {
  height: 100%;
  width: 2px;
  background-color: #e2e2e2;
}

.odd-time {
  background-color: #f2f2f2;
}

.horizontal-lines {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 3rem;
  width: 100%;
}

.horizontal-line {
  width: 100%;
  height: 2px;
  background-color: #e2e2e2;
}
</style>
