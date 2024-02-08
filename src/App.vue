<template>
  <div class="container">
    <div class="left">
      <div class="filler">SPRING 2024</div>
      <div class="days">
        <div class="day" v-for="(day, index) in schedule.days" :key="index">{{ day }}</div>
      </div>
    </div>
    <div class="right">
      <div class="times">
        <div class="time" v-for="(time, index) in schedule.timeline" :key="index">{{ time }}</div>
        <div class="time-lines">
          <div class="time-line" v-for="index in schedule.timeline.length" :key="index" />
        </div>
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
        <div class="class" />
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
  --horizontal-gap: 1rem; /* Adjust the gap between the vertical lines and the times (Width of the grid) */
  --vertical-gap: 4.5rem; /* Adjust the gap between the horizontal lines and the height of each day component (Height of the grid) */
  --components-gap: 1rem; /* Adjust the gap between each separated element (Semester Box, Times Box, Days Box, Grid Box) */
  --grid-gap: 2rem; /* Adjust the inline padding of the times and the vertical lines (Preferred to not change) */
  --top-height: 3rem; /* Adjust the height of the top components (Semester Box and Times Box) */
  --border-radius: 16px; /* The border radius of all components */
  --grid-color-primary: rgb(226, 226, 226);
  --grid-color-secondary: rgb(242, 242, 242);
  --line-thickness: 2px; /* (Preferred to not change) */
  --background: rgb(255, 255, 255, 0.4);
  --stroke: rgb(255, 255, 255, 0.3);
}

.container {
  display: flex;
  justify-content: center;
  width: auto;
  flex-direction: row;
  padding: var(--components-gap);
  gap: var(--components-gap);
  border-radius: calc(var(--border-radius) + var(--components-gap));
  backdrop-filter: blur(23px);
  background-color: var(--background);
  border: var(--line-thickness) solid var(--stroke);
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
  border: var(--line-thickness) solid var(--grid-color-primary);
  background-color: #fefefe;
  border-radius: var(--border-radius);
}

.times {
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  color: white;
  font-weight: 600;
  gap: var(--horizontal-gap);
  padding-inline: var(--grid-gap);
  height: var(--top-height);
  outline: var(--line-thickness) solid rgb(226, 226, 226, 0.8);
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.56) 0%, rgba(255, 255, 255, 0.23) 100%);
  border-radius: var(--border-radius);
  font-variant-numeric: tabular-nums;
}

.time {
  height: var(--top-height);
  display: flex;
  justify-content: center;
  align-items: center;
}

.time:nth-child(even) {
  color: rgb(58, 81, 139, 1);
  font-size: 12px;
}

.lines {
  display: flex;
  height: 100%;
  width: 100%;
  padding-inline: var(--grid-gap);
  justify-content: space-around;
  gap: var(--horizontal-gap);
}

.time-lines {
  position: absolute;
  display: flex;
  flex-direction: row;
  align-items: baseline;
  bottom: 0;
  padding-inline: var(--grid-gap);
  justify-content: space-around;
  gap: var(--horizontal-gap);
  width: 100%;
}

.time-line {
  width: var(--line-thickness);
  height: 12px;
  background-color: rgb(226, 226, 226, 0.62);
}

.time-line:nth-child(even) {
  height: 8px;
}

.left {
  display: flex;
  width: 10rem;
  flex-direction: column;
  gap: var(--components-gap);
}

.days {
  position: relative;
  border: var(--line-thickness) solid rgb(226, 226, 226, 0.62);
  border-radius: var(--border-radius);
  overflow: hidden;
}

.day {
  height: var(--vertical-gap);
  background-color: rgba(231, 234, 255, 0.192);
  color: white;
  font-weight: 600;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.day:first-child {
  border-radius: calc(var(--border-radius) - 2px) calc(var(--border-radius) - 2px) 0px 0px;
  border-bottom: 1px solid var(--stroke);
}

.day:not(:first-child):not(:last-child) {
  border-bottom: 1px solid var(--stroke);
  border-top: 1px solid var(--stroke);
}

.day:last-child {
  border-radius: 0px 0px calc(var(--border-radius) - 2px) calc(var(--border-radius) - 2px);
  border-top: 1px solid var(--stroke);
}

.filler {
  height: var(--top-height);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: var(--border-radius);
  color: white;
  font-weight: 600;
  background-color: rgb(29, 33, 89, 0.33);
  border: var(--line-thickness) solid rgb(29, 33, 89, 0.48);
}

.grid-container {
  background: red;
  height: 100%;
}

.grid-horizontal {
  height: 100%;
  width: var(--line-thickness);
  background-color: var(--grid-color-primary);
}

.odd-time {
  background-color: var(--grid-color-secondary);
}

.horizontal-lines {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: calc(var(--vertical-gap) - 2px);
  width: 100%;
}

.horizontal-line {
  width: 100%;
  height: var(--line-thickness);
  background-color: var(--grid-color-primary);
}

.class {
  position: absolute;
  height: var(--vertical-gap);
  width: 100%;
  background-color: rgba(143, 182, 255, 0.623);
  top: 0;
  left: 0;
}
</style>
