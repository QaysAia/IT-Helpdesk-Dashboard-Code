<!-- eslint-disable vue/multi-word-component-names -->
<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <div class="q-mx-md q-my-md row q-gutter-lg">
      <div style="width: 850px; height: 400px">
        <q-card class="my-card" style="height: 400px">
          <q-card-section>
            <div class="row">
              <div class="text-h6 text-bold" style="font-size: x-large">
                Tickets Status
              </div>

              <div class="q-item-section q-ml-auto">
                <q-btn icon="event" round color="primary">
                  <q-popup-proxy
                    @before-show="updateProxy"
                    cover
                    transition-show="scale"
                    transition-hide="scale"
                  >
                    <q-date v-model="model" range>
                      <div>
                        <q-btn
                          label="Cancel"
                          color="primary"
                          flat
                          v-close-popup
                        />
                        <q-btn
                          label="OK"
                          color="primary"
                          flat
                          @click="save"
                          v-close-popup
                        />
                      </div>
                    </q-date>
                  </q-popup-proxy>
                </q-btn>
              </div>
            </div>
            <br />
            <div class="flex flex-center">
              <apexchart
                type="bar"
                width="700"
                height="310"
                :options="chartOptions"
                :series="series"
              ></apexchart>
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div style="width: 850px; height: 400px">
        <q-card class="my-card" style="height: 400px">
          <q-card-section>
            <div class="row">
              <div
                class="text-h6 text-bold justify-start"
                style="font-size: x-large"
              >
                Tickets Per Category
              </div>
            </div>
            <div class="flex flex-center">
              <apexchart
                type="donut"
                width="450"
                :options="chartOptions2"
                :series="donut"
              ></apexchart>
            </div>
          </q-card-section>
        </q-card>
      </div>

      <div style="width: 850px; height: 30px">
        <q-card class="my-card" style="height: 400px">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              Tickets Activity
            </div>
            <div>
              <apexchart
                type="line"
                height="260"
                :options="chartOptions3"
                :series="lines"
              ></apexchart>
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div style="width: 850px; height: 30px">
        <q-card class="my-card" style="height: 400px">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              All Unresolved Tickets by Agents
            </div>
            <div>
              <apexchart
                type="bar"
                height="260"
                :options="chartOptions4"
                :series="bar"
              ></apexchart>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Dashboard",

  data() {
    return {
      series: [
        {
          name: "Net Profit",
          data: [44, 55, 57, 56, 61, 58, 63, 60, 66],
        },
        {
          name: "Revenue",
          data: [76, 85, 101, 98, 87, 105, 91, 114, 94],
        },
        {
          name: "Free Cash Flow",
          data: [35, 41, 36, 26, 45, 48, 52, 53, 41],
        },
      ],

      chartOptions: {
        chart: {
          type: "bar",
          height: 350,
        },
        plotOptions: {
          bar: {
            horizontal: false,
            columnWidth: "55%",
            endingShape: "rounded",
          },
        },
        dataLabels: {
          enabled: false,
        },
        stroke: {
          show: true,
          width: 2,
          colors: ["transparent"],
        },
        xaxis: {
          categories: [
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
          ],
        },
        yaxis: {
          title: {
            text: "$ (thousands)",
          },
        },
        fill: {
          opacity: 1,
        },
        tooltip: {
          y: {
            formatter: function (val) {
              return "$ " + val + " thousands";
            },
          },
        },
      },
    };
  },
});
</script>
