<!-- eslint-disable vue/multi-word-component-names -->
<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="row q-ml-lg q-mt-lg q-gutter-md">
    <div>
      <div>
        <q-card>
          <q-card-section>
            <div
              class="text-h6 text-center"
              style="font-size: x-large"
              flex-center
            >
              <h1 v-if="avarageTime">{{ avarageTime }}</h1>
              <q-spinner-hourglass color="purple" size="4em" v-else />
            </div>

            <br />
            <div></div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import moment from "moment";
const avarageTime = ref(null);

onMounted(() => {
  console.log("TESTA");
  const url =
    "https://it-helpdesk-mirdc.ap.ngrok.io/averageResponseTime?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=1";

  axios({
    method: "GET",
    url: url,
  }).then((response) => {
    console.log("qays", response.data[0].average_response_time);

    avarageTime.value = moment(response.data[0].average_response_time).format(
      "h:mm:ss"
    );
  });
});
</script>
