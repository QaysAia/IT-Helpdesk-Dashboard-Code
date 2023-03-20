<template>
  <div class="q-mx-md q-my-md row q-gutter-lg">
    <div style="width: 300px; height: 150px">
      <q-card class="my-card" style="height: 150px">
        <q-card-section>
          <div class="text-h6 text-bold" style="font-size: x-large">
            New Tickets
          </div>
          <br />
          <br />
          <div class="text-h6" style="font-size: 50px">6</div>
        </q-card-section>
      </q-card>
    </div>
    <div style="width: 300px; height: 50px">
      <q-card class="my-card" style="height: 150px">
        <q-card-section>
          <div class="text-h6 text-bold" style="font-size: x-large">
            Closed Tickets
          </div>
          <br />
          <br />
          <div class="text-h6" style="font-size: 50px">25</div>
        </q-card-section>
      </q-card>
    </div>
    <div style="width: 300px; height: 50px">
      <q-card class="my-card" style="height: 150px">
        <q-card-section>
          <div class="text-h6 text-bold" style="font-size: x-large">
            On Process
          </div>
          <br />
          <br />
          <div class="text-h6" style="font-size: 50px">5</div>
        </q-card-section>
      </q-card>
    </div>
    <div style="width: 300px; height: 50px">
      <q-card class="my-card" style="height: 150px">
        <q-card-section>
          <div class="text-h6 text-bold" style="font-size: x-large">
            Pending
          </div>
          <br />
          <br />
          <div class="text-h6" style="font-size: 50px">10</div>
        </q-card-section>
      </q-card>
    </div>
    <div style="width: 450px; height: 50px">
      <q-card class="my-card" style="height: 150px">
        <q-card-section>
          <div class="text-h6 text-bold" style="font-size: x-large">
            My Teams
          </div>
          <br />
          <div>
            <q-avatar
              v-for="n in 5"
              :key="n"
              size="45px"
              class="overlapping"
              :style="`right: ${n * 40}px`"
            >
              <img :src="`https://cdn.quasar.dev/img/avatar${n + 1}.jpg`" />
            </q-avatar>
          </div>
          <div>
            <q-avatar
              v-for="n in 4"
              :key="n"
              size="45px"
              class="overlapping"
              :style="`left: ${n * 40}px`"
            >
              <img :src="`https://cdn.quasar.dev/img/avatar${n + 1}.jpg`" />
            </q-avatar>
          </div>
        </q-card-section>
      </q-card>
    </div>
    <div style="width: 625px; height: 300px">
      <q-card class="my-card" style="height: 300px">
        <q-card-section>
          <div class="text-h6 text-bold" style="font-size: x-large">
            All Unresolved Tickets by Priority
          </div>
          <div class="flex flex-center">
            <apexchart
              type="pie"
              width="350"
              :options="chartOptions"
              :series="series"
            ></apexchart>
          </div>
        </q-card-section>
      </q-card>
    </div>
    <div style="width: 625px; height: 300px">
      <q-card class="my-card" style="height: 300px">
        <q-card-section>
          <div class="row">
            <div
              class="text-h6 text-bold justify-start"
              style="font-size: x-large"
            >
              Tickets Per Category
            </div>

            <div class="q-item-section q-ml-auto">
              <q-btn-dropdown color="primary" label="As of Today" size="11px">
                <q-list>
                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>As of Today</q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>Last 7 Days </q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>This Month</q-item-label>
                    </q-item-section>
                  </q-item>
                </q-list>
              </q-btn-dropdown>
            </div>

            <div class="q-item-section q-ml-auto">
              <q-btn-dropdown color="primary" label="All Division" size="11px">
                <q-list>
                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>Finance and Administration</q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label
                        >Materials and Product Research</q-item-label
                      >
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label
                        >Office of the Executive Director</q-item-label
                      >
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>Planning and Management</q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>Technology Diffusion</q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label
                        >ODED - Research and Development</q-item-label
                      >
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>Analysis and Testing</q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>Prototyping</q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>ODED - Technical Services</q-item-label>
                    </q-item-section>
                  </q-item>
                </q-list>
              </q-btn-dropdown>
            </div>
          </div>

          <div class="flex flex-center">
            <apexchart
              type="donut"
              height="310"
              width="417"
              :options="chartOptions2"
              :series="donut"
            ></apexchart>
          </div>

          <div class="text-subtitle2 text-lowercase text-right q-mr-xs q-pr-xs">
            <q-btn
              flat
              color="primary"
              label="more info"
              class="text-subtitle2 text-lowercase"
            />
          </div>
        </q-card-section>
      </q-card>
    </div>

    <div style="width: 450px; height: 30px">
      <q-card class="my-card" style="height: 300px">
        <q-card-section>
          <div>
            <q-btn unelevated color="black" label="last 7 days"></q-btn>
          </div>
          <br />
          <div
            class="text-h6 text-center"
            style="font-size: x-large"
            flex-center
          >
            Average First Response Time
          </div>
          <br />
          <div
            class="text-h6 text-center"
            style="font-size: xx-large"
            flex-center
          >
            4h 15min
          </div>
          <br />
          <div
            class="text-h6 text-center"
            style="font-size: x-large"
            flex-center
          >
            Average Resolution Time
          </div>
          <br />
          <div
            class="text-h6 text-center"
            style="font-size: xx-large"
            flex-center
          >
            4h 15min
          </div>
        </q-card-section>
      </q-card>
    </div>

    <div style="width: 625px; height: 30px">
      <q-card class="my-card" style="height: 320px">
        <q-card-section>
          <div class="row">
            <div
              class="text-h6 text-bold justify-start"
              style="font-size: x-large"
            >
              Tickets Activity
            </div>

            <div class="q-item-section q-ml-auto">
              <q-btn-dropdown color="primary" label="Months" size="11px">
                <q-list>
                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>As of Today</q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>Last 7 Days </q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section>
                      <q-item-label>This Month</q-item-label>
                    </q-item-section>
                  </q-item>
                </q-list>
              </q-btn-dropdown>
            </div>
          </div>
          <br />
          <div class="flex flex-center">
            <apexchart
              type="line"
              height="230"
              width="600"
              :options="chartOptions3"
              :series="lines"
            ></apexchart>
          </div>
        </q-card-section>
      </q-card>
    </div>
    <div style="width: 625px; height: 30px">
      <q-card class="my-card" style="height: 320px">
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
    <div style="width: 450px; height: 30px">
      <q-card class="my-card" style="height: 320px">
        <q-card-section>
          <div class="text-h5 text-bold">Leaderboard</div>
          <div>This Month</div>
          <br />
          <div style="text-align: center">
            <img
              :src="`https://cdn.quasar.dev/img/avatar${4}.jpg`"
              style="
                width: 130px;
                height: 130px;
                border-radius: 50%;
                box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2),
                  0 6px 20px 0 rgba(0, 0, 0, 0.19);
                position: absolute;
                top: 90%;
                left: 10%;
              "
            />
          </div>
          <div
            style="
              position: absolute;
              top: 225%;
              left: 24%;
              transform: translate(-50%, -50%);
            "
          >
            <img
              src="~assets\award_star.png"
              style="width: 85px; height: 85px"
            />
          </div>
        </q-card-section>
        <br />
        <br />
        <div
          class="text-h6 text-right text-bold q-mr-xl"
          style="font-size: x-large"
        >
          Qays Khairy Gadat
        </div>
        <div
          class="text-h6 text-right text-bold q-mr-xl q-pr-md"
          style="font-size: large; color: blueviolet"
        >
          Top Performer Agent
        </div>
      </q-card>
    </div>
  </div>
</template>

<style lang="sass" scoped>
.overlapping
  border: 2px solid white
  position: absolute
</style>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",

  data() {
    return {
      series: [20, 13, 9, 3],
      chartOptions: {
        chart: {
          width: 380,
          type: "pie",
        },
        labels: ["Low", "Medium", "High", "Urgent"],
        responsive: [
          {
            breakpoint: 480,
            options: {
              chart: {
                width: 200,
              },
              legend: {
                position: "bottom",
              },
            },
          },
        ],
      },
      donut: [15, 25, 10, 6, 9, 5, 5, 20, 6],
      chartOptions2: {
        chart: {
          width: 1000,
          type: "donut", // change the chart type to "donut"
        },
        labels: [
          "System Error",
          "Network Access",
          "Account Access",
          "Hardware Devices",
          "Software Installation",
          "System Modification",
          "System Development",
          "Technical Assistance",
          "Website Post",
        ], // add a new label for the new data point
        responsive: [
          {
            breakpoint: 480,
            options: {
              chart: {
                width: 1000,
              },
              legend: {
                position: "bottom",
              },
            },
          },
        ],
      },

      lines: [
        {
          name: "Tickets",
          data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
        },
      ],
      chartOptions3: {
        chart: {
          height: 350,
          type: "line",
          zoom: {
            enabled: false,
          },
        },
        stroke: {
          curve: "straight",
        },
        title: {
          text: "Tickets by Month",
          align: "left",
        },
        grid: {
          row: {
            colors: ["#f3f3f3", "transparent"], // takes an array which will be repeated on columns
            opacity: 0.5,
          },
        },
        xaxis: {
          categories: [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
          ],
        },
      },

      bar: [
        {
          data: [10, 5, 3, 1, 12, 5, 7, 6, 1],
        },
      ],
      chartOptions4: {
        chart: {
          type: "bar",
          height: 350,
        },
        plotOptions: {
          bar: {
            borderRadius: 4,
            horizontal: true,
          },
        },
        dataLabels: {
          enabled: false,
        },
        xaxis: {
          categories: [
            "Qays Khairy Gadat",
            "John Lloyd Etoc",
            "Kai Sotto",
            "Lebron James",
            "Kevin Durant",
            "Steph Curry",
            "Kyrie Irving",
            "Derick Rose",
            "Ja Morant",
            "Kobe Bryant",
          ],
        },
      },
    };
  },
});
</script>
