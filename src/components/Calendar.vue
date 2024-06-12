<script setup lang="ts">
import moment from 'moment';

const weekDays = moment.weekdays();

interface ResponseGetDays {
  dayMonth: string;
  name: string;
  weekDay: number;
  weekMonth: number;
  currentMonth: boolean;
}


const getDaysInMonth = (): ResponseGetDays[] => {
  const currentMonth = moment().month();
  const currentYear = moment().year();
  const daysInMonth = moment().daysInMonth();
  const daysOfMonth = [];

  for (let i = 1; i <= daysInMonth; i++) {
    const day = moment().month(currentMonth).year(currentYear).date(i); // 1

    if(i === 1 && day.day() !== 0) {
      const daysToSubtract = day.day();
      const referenceDate = moment(day).subtract(daysToSubtract, 'days');

      for (let x = 0; x < daysToSubtract; x++) {
        const date = moment(referenceDate).add(x, 'days');
        daysOfMonth.push({
          dayMonth: date.format('D'),
          name: date.format('dddd'),
          weekDay: date.day(),
          weekMonth: date.week(),
          currentMonth: false,
        });
      }
    }

    daysOfMonth.push({
      dayMonth: day.format('D'),
      name: day.format('dddd'),
      weekDay: day.day(),
      weekMonth: day.week(),
      currentMonth: true,
    });

    if(i === daysInMonth && day.day() !== 6) {
      const daysToAdd = 6 - day.day();
      for (let x = 1; x <= daysToAdd; x++) {
        const date = moment(day).add(x, 'days');
        daysOfMonth.push({
          dayMonth: date.format('D'),
          name: date.format('dddd'),
          weekDay: date.day(),
          weekMonth: date.week(),
          currentMonth: false,
        });
      }
    }

  }

  return daysOfMonth;
}

</script>

<template>

  <div class="flex-container pt-3">

    <div class="label-day" v-for="(day, index) in weekDays" :key="index">
      <span> {{day}} </span>
    </div>

  </div>

    <div class="flex-container">

      <div class="box-day" v-for="(day, index) in getDaysInMonth()" :key="index"
           @click="console.log(day)">

        <span class="span-weekend-day" v-if="day.currentMonth && (day.weekDay === 0 || day.weekDay === 6)">
          {{day.dayMonth}}
        </span>

        <span class="span-week-day" v-if="day.currentMonth && (day.weekDay !== 0 && day.weekDay !== 6)">
          {{day.dayMonth}}
        </span>

        <span class="span-not-current-month" v-if="!day.currentMonth">
          {{day.dayMonth}}
        </span>
      </div>

    </div>


</template>

<style scoped>
  .flex-container {
    display: flex;
    flex-wrap: wrap;
  }

  .label-day {
    border: 1px solid #fff;
    background-color: #2F74B7;
    flex: 1 0 14%;
    text-align: center;
    margin: 0;
    line-height: 50px;
    color: #fff;
  }

  .box-day {
    flex: 1 0 14%;
    border: 1px solid #ccc;
    text-align: center;
    height: 120px;
    margin: 0;
  }

  .span-weekend-day {
    color: #0d2ae7;
  }

  .span-week-day {
    color: #000000;
  }

  .span-not-current-month {
    color: #cccccc;
  }

</style>