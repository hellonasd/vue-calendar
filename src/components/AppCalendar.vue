<template>
  <div class="calendar-main">
    <app-calendar-header></app-calendar-header>
    <app-date
      :value="value"
      @next="next"
      @prev="prev"
      @today="today"
    ></app-date>
    <div class="days">
      <div class="days__day" v-for="day in days" :key="day">{{ day }}</div>
    </div>
    <div class="calendar">
      <div
        v-for="(day, index) in calendar"
        :key="index"
        class="calendar__weeks"
        :class="[weeksDays(day)]"
      >
        <div class="calendar__wrapper">
          <span class="calendar__day" :class="[currentDay(day) ? 'today' : '']">
            {{ day.format("D") }}
          </span>
          <span class="calendar__day-month" v-if="mon">{{ mon }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import AppCalendarHeader from "@/components/AppCalendarHeader";
import appDate from "@/components/appDate";

moment.locale("ru");
export default {
  data() {
    return {
      days: ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"],
      day: null,
      startDay: null,
      endDay: null,
      value: moment(),
      calendar: [],
      mon: null,
      styleBefore: "",
    };
  },
  mounted() {
    this.calendarCreate(this.value);
  },
  methods: {
    calendarCreate(value) {
      this.calendar = [];
      this.startDay = value
        .clone()
        .startOf("month")
        .startOf("week")
        .isoWeekday(1);
      this.day = this.startDay.clone().subtract(1, "day");
      this.calendar = [...Array(42)].map(() => this.day.add(1, "day").clone());
    },

    next() {
      this.calendarCreate(this.value.add(1, "month"));
    },
    today() {
      this.value = moment();
      this.calendarCreate(this.value);
    },
    prev() {
      this.calendarCreate(this.value.subtract(1, "month"));
    },
    currentDay(day) {
      return moment().isSame(day, "day");
    },
    weeksDays(day) {
      return day.day() === 6 || day.day() === 0 ? "weekends" : "";
    },
  },
  components: { AppCalendarHeader, appDate },
};
</script>

<style lang='scss'>
.weekends {
  background-color: #272829;
}

.days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  justify-items: end;
  margin-bottom: 5px;
  &__day {
    color: white;
    font-size: 20px;
  }
}
.calendar-main {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;

  background-color: #20242b;
}
.calendar {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  overflow: hidden;
  height: 100%;

  &__weeks {
    width: 100%;
    border: 1px solid rgb(64, 64, 64);
  }
  &__wrapper {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 5px;
  }
  &__day {
    display: flex;
    color: rgb(214, 215, 216);
    font-size: 19px;
    font-family: monospace;

    &.today {
      background-color: rgb(237, 70, 54);

      width: 25px;
      height: 25px;
      border-radius: 50%;
      justify-content: center;
      align-items: center;
    }
  }
  &__day-month {
    font-size: 18px;
    font-family: sans-serif;
    color: rgb(214, 215, 216);
  }
}
</style>
