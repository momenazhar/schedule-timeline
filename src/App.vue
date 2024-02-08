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
        <div class="classes-container">
          <div class="class sat">
            <div
              v-if="shouldRenderBox('sat')"
              v-for="(day, index) in schedule.classes.sat"
              :key="index"
            >
              <div
                class="classbox"
                :style="{
                  left: calculateLeft(day.start),
                  width: calculateWidth(day.end, day.start)
                }"
              >
                {{ day.name }}
                <div class="section">{{ day.section }}</div>
                <div class="info">SAT {{ day.start }} - {{ day.end }} | {{ day.location }}</div>
              </div>
            </div>
          </div>
          <div class="class sun">
            <div
              v-if="shouldRenderBox('sun')"
              v-for="(day, index) in schedule.classes.sun"
              :key="index"
            >
              <div class="box">
                <div
                  class="classbox"
                  :style="{
                    left: calculateLeft(day.start),
                    width: calculateWidth(day.end, day.start),
                    ...setRandomColor()
                  }"
                >
                  {{ day.name }}
                  <div class="section">{{ day.section }}</div>
                  <div class="info">SUN {{ day.start }} - {{ day.end }} | {{ day.location }}</div>
                </div>
              </div>
            </div>
          </div>
          <div class="class mon">
            <div
              v-if="shouldRenderBox('mon')"
              v-for="(day, index) in schedule.classes.mon"
              :key="index"
            >
              <div class="box">
                <div
                  class="classbox"
                  :style="{
                    left: calculateLeft(day.start),
                    width: calculateWidth(day.end, day.start),
                    ...setRandomColor()
                  }"
                >
                  {{ day.name }}
                  <div class="section">{{ day.section }}</div>
                  <div class="info">MON {{ day.start }} - {{ day.end }} | {{ day.location }}</div>
                </div>
              </div>
            </div>
          </div>
          <div class="class tue">
            <div
              v-if="shouldRenderBox('tue')"
              v-for="(day, index) in schedule.classes.tue"
              :key="index"
            >
              <div class="box">
                <div
                  class="classbox"
                  :style="{
                    left: calculateLeft(day.start),
                    width: calculateWidth(day.end, day.start),
                    ...setRandomColor()
                  }"
                >
                  {{ day.name }}
                  <div class="section">{{ day.section }}</div>
                  <div class="info">TUE {{ day.start }} - {{ day.end }} | {{ day.location }}</div>
                </div>
              </div>
            </div>
          </div>
          <div class="class wed">
            <div
              v-if="shouldRenderBox('wed')"
              v-for="(day, index) in schedule.classes.wed"
              :key="index"
            >
              <div class="box">
                <div
                  class="classbox"
                  :style="{
                    left: calculateLeft(day.start),
                    width: calculateWidth(day.end, day.start),
                    ...setRandomColor()
                  }"
                >
                  {{ day.name }}
                  <div class="section">{{ day.section }}</div>
                  <div class="info">WED {{ day.start }} - {{ day.end }} | {{ day.location }}</div>
                </div>
              </div>
            </div>
          </div>
          <div class="class thu">
            <div
              v-if="shouldRenderBox('thu')"
              v-for="(day, index) in schedule.classes.thu"
              :key="index"
            >
              <div class="box">
                <div
                  class="classbox"
                  :style="{
                    left: calculateLeft(day.start),
                    width: calculateWidth(day.end, day.start),
                    ...setRandomColor()
                  }"
                >
                  {{ day.name }}
                  <div class="section">{{ day.section }}</div>
                  <div class="info">THU {{ day.start }} - {{ day.end }} | {{ day.location }}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// !!!!! Weird calculations here to calculate padding
const gridGap =
  (parseFloat(getComputedStyle(document.documentElement).getPropertyValue('--grid-gap')) +
    parseFloat(getComputedStyle(document.documentElement).getPropertyValue('--horizontal-gap'))) *
    16 +
  5.8

export default {
  data() {
    return {
      schedule: {
        classes: {
          sun: [
            {
              name: 'Operating Systems',
              start: '08:00',
              end: '09:30',
              location: 'B-B01',
              section: 'T1'
            },
            {
              name: 'OOP',
              start: '12:00',
              end: '14:00',
              location: 'B-B01',
              section: 'T2'
            }
          ],
          tue: [
            {
              name: 'Management of Medically Compromised Patients',
              start: '08:00',
              end: '10:00',
              location: 'B-B01',
              section: 'L1'
            }
          ]
        },
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
          '13:00',
          '13:30',
          '14:00',
          '14:30',
          '15:00',
          '15:30',
          '16:00',
          '16:30',
          '17:00',
          '17:30',
          '18:00'
        ],
        days: ['SATURDAY', 'SUNDAY', 'MONDAY', 'TUESDAY', 'WEDNESDAY', 'THURSDAY']
      }
    }
  },
  methods: {
    shouldRenderBox(day) {
      // Check if there are any classes for the specified day
      return this.schedule.classes.hasOwnProperty(day) && this.schedule.classes[day].length > 0
    },
    calculateLeft(startTime) {
      // Calculate the left position based on the start time
      const timeIndex = this.schedule.timeline.indexOf(startTime)
      if (timeIndex !== -1) {
        return `${timeIndex * 57.7 + gridGap}px`
      }
      return '0px' // Default value
    },
    calculateWidth(endTime, startTime) {
      const timeIndexStart = this.schedule.timeline.indexOf(startTime)
      const timeIndexEnd = this.schedule.timeline.indexOf(endTime)

      if (timeIndexStart !== -1 && timeIndexEnd !== -1) {
        // Calculate the total width available between the start and end times
        const totalWidth = (timeIndexEnd - timeIndexStart) * 57.7 - 2 // Adjusted width considering the gap

        return `${totalWidth}px`
      }

      return '0px' // Default value
    },
    // Function to generate a random rgba color code with 50% opacity
    getRandomColor() {
      const randomColor = Math.floor(Math.random() * 16777215).toString(16)
      return '#' + randomColor
    },

    // Function to set both background and border color using the same random color
    setRandomColor() {
      const randomColor = this.getRandomColor()
      return {
        background: `linear-gradient(90deg, rgba(${parseInt(randomColor.slice(-6, -4), 16)}, ${parseInt(randomColor.slice(-4, -2), 16)}, ${parseInt(randomColor.slice(-2), 16)}, 0.30) 0%, rgba(${parseInt(randomColor.slice(-6, -4), 16)}, ${parseInt(randomColor.slice(-4, -2), 16)}, ${parseInt(randomColor.slice(-2), 16)}, 0.25) 10%)`,
        borderColor: randomColor,
        color: randomColor
      }
    }
  }
}
</script>

<style>
:root {
  --horizontal-gap: 1rem; /* Adjust the gap between the vertical lines and the times (Width of the grid) */
  --vertical-gap: 5rem; /* Adjust the gap between the horizontal lines and the height of each day component (Height of the grid) */
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

.classes-container {
  position: absolute;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  border-radius: calc(var(--border-radius) - 2px);
  height: 100%;
  width: 100%;
}

.class {
  position: relative;
  display: flex;
  height: var(--vertical-gap);
  width: 100%;
}

.box {
  display: flex;
  align-items: center;
  height: 100%;
}

.classbox {
  position: absolute;
  height: 90%;
  border-radius: var(--border-radius);
  backdrop-filter: blur(3px);
  border-left: 4px solid;
  padding: 8px;
  font-size: 12px;
  font-weight: 600;
  overflow: hidden;
}

.section {
  position: absolute;
  top: 0;
  right: 0;
  width: 2rem;
  text-align: center;
  background: inherit;
  font-size: 16px;
  padding: 6px;
  border-radius: 0 0 0 var(--border-radius);
}

.info {
  position: absolute;
  color: white;
  font-weight: 500;
  font-size: 10px;
  bottom: 10px;
}
</style>
