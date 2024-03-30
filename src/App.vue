<script setup>
import { ref } from 'vue'
// fix this with docker ip and port you setting in container
const apiHostname = 'http://localhost:8080' 
const URL = `${apiHostname}/api/v1/drivers/2022`
const requestOptions = {
  method: "GET",
  redirect: "follow"
};

const driverArr = ref([])
fetch(URL, requestOptions)
  .then((response) => response.json())
  .then((result) => {
    driverArr.value.push(...result)
  }) 
  .catch((error) => console.error(error));

</script>

<template>
  <div>
    <h1>Formula 1 Drivers Line-up in 2022</h1>
    <ul v-for="(driver, index) in driverArr">
      <li>
        {{ index + 1}}. {{ driver.fullname }} – Cars number {{ driver.driver_number }}
      </li>
    </ul>
  </div>
  <p>Endpoints</p>
  <p>API HOSTNAME : {{ apiHostname }}</p>
  <p>API Endpoint : {{ URL }}</p>
</template>
