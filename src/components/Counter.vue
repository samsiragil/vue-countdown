<script setup>
  import {reactive,ref,onMounted} from 'vue'
  import moment from 'moment'

  const countdown = ref(moment())
  const timeout = ref(false)
  const deadline = ref(moment().set({'year': 2023, 'month': 11, 'date': 3, 'hour': 0, 'minute': 0, 'second': 0}))
  const setupCounter = () =>{
    let now = moment()
    countdown.value = moment.duration(moment(deadline.value).diff(moment(now)))
    let looping = setInterval(() => {
      countdown.value = countdown.value.subtract(1, 'seconds')
      if (countdown.value.months() <= 0 && countdown.value.weeks() <= 0 && countdown.value.hours() <= 0 && countdown.value.minutes() <= 0 && countdown.value.seconds() <= 0) {
        clearInterval(looping)
        timeout.value = true
      }
    },1000)
  }

  const constFormatNumber = (data) => {
    return data < 10 ? `0${data}` : data
  }

  onMounted(()=>{
    setupCounter()
  })
</script>

<template>
  <div class="container-fluid">
    <div class="w-100 no-ws">
      <p class="mb-0 counter-item timer time">{{ constFormatNumber(countdown.months()) }}</p>
      <p class="mb-0 counter-item timer separator">:</p>
      <p class="mb-0 counter-item timer time">{{ constFormatNumber(countdown.days()) }}</p>
      <p class="mb-0 counter-item timer separator">:</p>
      <p class="mb-0 counter-item timer time">{{ constFormatNumber(countdown.hours()) }}</p>
      <p class="mb-0 counter-item timer separator">:</p>
      <p class="mb-0 counter-item timer time">{{ constFormatNumber(countdown.minutes()) }}</p>
      <p class="mb-0 counter-item timer separator">:</p>
      <p class="mb-0 counter-item timer time">{{ constFormatNumber(countdown.seconds()) }}</p>
    </div>
    <div class="w-100 no-ws mb-3">
      <p class="mb-0 counter-item label time">MONTHS</p>
      <p class="mb-0 counter-item label separator"></p>
      <p class="mb-0 counter-item label time">DAYS</p>
      <p class="mb-0 counter-item label separator"></p>
      <p class="mb-0 counter-item label time">HOURS</p>
      <p class="mb-0 counter-item label separator"></p>
      <p class="mb-0 counter-item label time">MINUTES</p>
      <p class="mb-0 counter-item label separator"></p>
      <p class="mb-0 counter-item label time">SECONDS</p>
    </div>
  </div>
</template>
