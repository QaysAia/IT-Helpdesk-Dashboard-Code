<template>
  <!-- <div class="row q-mx-md q-my-md q-gutter-md"> -->
  <div>
    <div class="row flex flex-center q-mt-sm q-pa-md">
      <div class="col-lg-2 col-md-4 q-mr-md q-mt-sm">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              New Tickets
            </div>
            <br />
            <br />
            <div class="text-h6" style="font-size: 50px">{{ newTickets }}</div>
          </q-card-section>
        </q-card>
      </div>
      <div class="col-lg-2 col-md-4 q-mr-md q-mt-sm">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              For Eval
            </div>
            <br />
            <br />
            <div class="text-h6" style="font-size: 50px">
              {{ forEvalTickets }}
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div class="col-lg-2 col-md-4 q-mr-md q-mt-sm">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              On Process
            </div>
            <br />
            <br />
            <div class="text-h6" style="font-size: 50px">
              {{ ongoingTickets }}
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div class="col-lg-2 col-md-4 q-mr-md q-mt-sm">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              Pending
            </div>
            <br />
            <br />
            <div class="text-h6" style="font-size: 50px">
              {{ pendingTickets }}
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div class="col-lg-3 col-md-4 q-mr-md q-mt-sm">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              Closed Tickets
            </div>
            <br />
            <br />
            <div class="text-h6" style="font-size: 50px">
              {{ closedTickets }}
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
    <div class="row flex flex-center q-mt-xs">
      <div
        v-if="!$q.screen.lt.md"
        class="col-lg-4 col-10 q-mr-md q-mt-xs print-media"
      >
        <q-card class="my-card" style="height: 345px">
          <q-card-section>
            <div class="row">
              <div class="q-pa-xs" style="max-width: 300px">
                <div class="q-gutter-sm">
                  <div class="text-h6 text-bold" style="font-size: x-large">
                    Tickets by Area
                  </div>
                </div>
              </div>

              <div class="q-pa-xs q-ml-xl q-mr-none" style="max-width: 300px">
                <div class="q-gutter-sm q-ml-xl"></div>
              </div>

              <div class="q-pa-xs q-ml-xl" style="max-width: 230px">
                <div class="q-gutter-sm q-ml-md">
                  <q-select
                    v-model="model1"
                    :options="options1"
                    stack-label
                    label="Tickets Filter"
                    @update:model-value="(value) => ticketsByDivision(value)"
                  >
                    <template v-if="model1" v-slot:selected>
                      <p class="q-my-none q-ml-xs q-mr-none text-weight-bolder">
                        {{ model1.label }}
                      </p>
                    </template>
                  </q-select>
                </div>
              </div>
            </div>

            <div v-if="!loadingTicketByArea" class="flex flex-center">
              <apexchart
                type="donut"
                height="400"
                width="450"
                :options="chartOptions1"
                :series="donut"
              ></apexchart>
            </div>

            <div v-if="loadingTicketByArea" class="flex flex-center q-pa-md">
              <div>
                <q-skeleton type="QAvatar" size="210px" />
              </div>
              <div class="q-ml-xl">
                <q-skeleton width="150px" />
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>

      <div
        v-if="!$q.screen.lt.md"
        class="col-lg-4 col-10 q-mr-md q-mt-sm print-media2"
      >
        <q-card class="my-card" style="height: 345px">
          <q-card-section>
            <div class="row">
              <div class="q-pa-xs" style="max-width: 300px">
                <div class="q-gutter-sm">
                  <div class="text-h6 text-bold" style="font-size: x-large">
                    Tickets by Category
                  </div>
                </div>
              </div>
            </div>
            <br />

            <div v-if="!loading" class="flex flex-center">
              <apexchart
                type="pie"
                height="400"
                width="450"
                :options="chartOptions2"
                :series="donut1"
              ></apexchart>
            </div>

            <div v-if="loading" class="flex flex-center q-pa-md">
              <div>
                <q-skeleton type="QAvatar" size="210px" />
              </div>
              <div class="q-ml-xl">
                <q-skeleton width="150px" />
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>

      <div class="col-lg-3 col-10 q-mr-md q-mt-sm print-media3">
        <q-card class="my-card" style="height: 345px">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              All Tickets
            </div>
            <div class="flex flex-center">
              <div class="flex flex-center">
                <apexchart
                  type="radialBar"
                  width="360"
                  :options="chartOptions"
                  :series="series"
                ></apexchart>
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>

    <div class="row flex flex-center q-mt-xs">
      <div
        v-if="!$q.screen.lt.md"
        class="col-lg-4 col-10 q-mr-md q-mt-md print-media4"
      >
        <q-card class="my-card" style="height: 320px">
          <q-card-section>
            <div class="row">
              <div class="q-pa-xs" style="max-width: 300px">
                <div class="q-gutter-sm">
                  <div class="text-h6 text-bold" style="font-size: x-large">
                    Clients by Category
                  </div>
                </div>
              </div>
            </div>

            <div v-if="!loading" class="flex flex-center">
              <apexchart
                type="pie"
                height="400"
                width="450"
                :options="labelClientsCategory"
                :series="pieClientsCategory"
              ></apexchart>
            </div>

            <div v-if="loading" class="flex flex-center q-pa-md">
              <div>
                <q-skeleton type="QAvatar" size="210px" />
              </div>
              <div class="q-ml-xl">
                <q-skeleton width="150px" />
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
      <!-- <div class="col-lg-4 col-10 q-mr-md q-mt-md">
        <q-card class="my-card" style="height: 320px">
          <q-card-section>
            <div class="row">
              <div
                class="text-h6 text-bold justify-start"
                style="font-size: x-large"
              >
                Clients by Category
              </div>

              <div class="q-item-section q-ml-auto"></div>
            </div>
            <br />

            <div class="flex flex-center">
              <apexchart
                type="donut"
                height="400"
                width="450"
                :options="chartOptions2"
                :series="donut1"
              ></apexchart>
            </div>
          </q-card-section>
        </q-card>
      </div> -->

      <div class="col-lg-4 col-10 q-mr-md q-mt-md print-media3">
        <q-card class="my-card" style="height: 320px">
          <q-card-section>
            <div class="text-h6 text-bold" style="font-size: x-large">
              All Clients
            </div>

            <div class="flex flex-center">
              <apexchart
                type="radialBar"
                width="400"
                height="280"
                :options="allTotalClients"
                :series="allClients"
              ></apexchart>
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div class="col-lg-3 col-10 q-mr-md q-mt-md print-media4">
        <q-card class="my-card" style="height: 320px">
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
              {{ averageTime }}
            </div>
            <br />
            <!-- <div
              class="text-h6 text-center"
              style="font-size: x-large"
              flex-center
            >
              Average Resolution Time
            </div>
            <br />
            <div
              v-if="!loading"
              class="text-h6 text-center"
              style="font-size: xx-large"
              flex-center
            >
              {{ averageRESTime }}
            </div> -->
            <!-- <div v-if="loading" class="flex flex-center">
              <q-spinner color="primary" size="5em" :thickness="10" />
            </div> -->
          </q-card-section>
        </q-card>
      </div>
    </div>
    <br />

    <div class="flex flex-center q-mt-xs print-media5">
      Copyright © 2022 PMD-MIS. All rights reserved.
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import { Screen } from "quasar";
import axios from "axios";
import moment from "moment";
import { ref } from "vue";
const qs = require("qs");

export default defineComponent({
  name: "IndexPage",

  data() {
    return {
      model: ref({
        label: "All Division",
        value: "",
      }),

      model1: ref({
        label: "All Division",
        value: "",
      }),

      options1: [
        {
          label: "All Division",
          value: "",
        },
        {
          label: "Analysis and Testing Division",
          value: "ATD",
        },
        {
          label: "Finance and Administrative Division",
          value: "FAD",
        },
        {
          label: "Materials and Process Research Division",
          value: "MPRD",
        },
        {
          label: "ODED - Research and Development",
          value: "ODED-RD",
        },
        {
          label: "ODED - Technical Services",
          value: "ODED-TS",
        },
        {
          label: "Office of the Executive Director",
          value: "OED",
        },
        {
          label: "Prototyping Division",
          value: "PD",
        },
        {
          label: "Planning and Managment Division",
          value: "PMD",
        },
        {
          label: "Technology Diffusion Division",
          value: "TDD",
        },
      ],

      // model1: ref({
      //   label: "Clients by Category",
      //   value: "goog",
      // }),

      // options1: [
      //   {
      //     label: "Clients by Category",
      //     value: "goog",
      //   },
      //   {
      //     label: "Clients by Area",
      //     value: "fb",
      //   },
      // ],

      ticketsData: [],
      NewTickets: 0,
      Closed: 0,
      ForEval: 0,
      Pending: 0,
      Ongoing: 0,
      averageTime: 0,
      averageRESTime: 0,
      loading: false, // Initialize loading state to false
      loadingTicketByArea: false, // Initialize loading state to false
      // Your other data properties here

      series: [],
      chartOptions: {
        chart: {
          height: 300,
          type: "radialBar",
          toolbar: {
            show: true,
          },
        },

        plotOptions: {
          radialBar: {
            startAngle: -150,
            endAngle: 210,
            hollow: {
              margin: 0,
              size: "70%",
              background: "#fff",
              image: undefined,
              imageOffsetX: 0,
              imageOffsetY: 0,
              position: "front",
              dropShadow: {
                enabled: true,
                top: 3,
                left: 0,
                blur: 4,
                opacity: 0.24,
              },
            },
            track: {
              background: "#fff",
              strokeWidth: "67%",
              margin: 0, // margin is in pixels
              dropShadow: {
                enabled: true,
                top: -3,
                left: 0,
                blur: 4,
                opacity: 0.35,
              },
            },

            dataLabels: {
              show: true,
              name: {
                offsetY: -10,
                show: true,
                color: "#888",
                fontSize: "17px",
              },
              value: {
                formatter: function (val) {
                  return parseInt(val);
                },
                color: "#111",
                fontSize: "36px",
                show: true,
              },
            },
          },
        },

        fill: {
          type: "gradient",
          gradient: {
            shade: "dark",
            type: "horizontal",
            shadeIntensity: 0.5,
            gradientToColors: ["#ABE5A1"],
            inverseColors: true,
            opacityFrom: 1,
            opacityTo: 1,
            stops: [0, 100],
          },
        },
        stroke: {
          lineCap: "round",
        },
        labels: ["Tickets"],
      },

      donut: [
        {
          data: [],
        },
      ],

      chartOptions1: {
        value: {
          formatter: function (val) {
            return parseInt(val);
          },
          color: "#111",
          fontSize: "36px",
          show: true,
        },
        chart: {
          width: 1000,
          type: "donut",
        },
        labels: [],
        dataLabels: {
          formatter: function (val, opts) {
            return opts.w.config.series[opts.seriesIndex];
          },
        },
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

      donut1: [
        {
          data: [],
        },
      ],

      chartOptions2: {
        dataLabels: {
          formatter: function (val, opts) {
            return opts.w.config.series[opts.seriesIndex];
          },
        },

        color: "#111",
        fontSize: "36px",
        show: true,

        chart: {
          width: 1000,
          type: "donut",
        },

        labels: [],

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

      pieClientsCategory: [
        {
          data: [],
        },
      ],
      labelClientsCategory: {
        dataLabels: {
          enabled: true,
        },

        dataLabels: {
          formatter: function (val, opts) {
            return opts.w.config.series[opts.seriesIndex];
          },
        },

        chart: {
          width: 380,
          type: "pie",
        },

        labels: [],
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

      ticketsData1: [],

      allClients: [],
      allTotalClients: {
        chart: {
          height: 400,

          type: "radialBar",
        },
        plotOptions: {
          radialBar: {
            hollow: {
              size: "50%",
            },
            dataLabels: {
              value: {
                formatter: function (value) {
                  return parseInt(value);
                },
                show: true,
                suffix: "",
                fontSize: "20px",
                fontWeight: "bold",
              },
            },
          },
        },
        labels: ["Clients"],
      },

      bar: [
        {
          name: "Total Number",
          data: [],
        },
      ],
      chartOptionbar: {
        chart: {
          height: 350,
          type: "bar",
        },
        plotOptions: {
          bar: {
            borderRadius: 0,
            columnWidth: "40%",
          },
        },
        dataLabels: {
          enabled: false,
        },
        stroke: {
          width: 0,
        },

        grid: {
          row: {
            colors: ["#fff", "#f2f2f2"],
          },
        },

        xaxis: {
          labels: {
            style: {
              fontSize: "9px",
            },
            rotate: -30,
          },
          categories: [],
        },
      },
    };
  },

  created() {
    this.fetchTickets();
  },
  methods: {
    async ticketsByDivision() {
      console.log("query", this.model1.value);
      this.loadingTicketByArea = true;
      const urlticketsByDivision = `https://it-helpdesk-mirdc.ap.ngrok.io/ticketsByCategory?from=2023/01/01&to=2023/12/31&projID=38&division=${this.model1.value}`;

      const responseticketsByDivision = await axios({
        method: "GET",
        url: urlticketsByDivision,
      });
      this.donut = responseticketsByDivision.data.map((cat) => cat.tickets) || {
        0: 0,
      };
      this.chartOptions1.labels = responseticketsByDivision.data.map(
        (cat) => cat.category_name
      );
      this.loadingTicketByArea = false;
      console.log("this.donut", this.donut);
    },

    async fetchTickets() {
      const url4 =
        "https://it-helpdesk-mirdc.ap.ngrok.io/ticketsForProj?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=38";

      const response4 = await axios({
        method: "GET",
        url: url4,
      });
      this.ticketsData1 = await response4.data;
      console.log("response4", this.ticketsData1);
    },
  },

  computed: {
    ongoingTickets() {
      return this.ticketsData1
        .filter((ticket) => ticket.status.trim() === "Ongoing")
        .map((ticket) => ticket.tickets)
        .reduce((total, tickets) => total + tickets, 0);
    },
    closedTickets() {
      return this.ticketsData1
        .filter((ticket) => ticket.status.trim() === "Closed")
        .map((ticket) => ticket.tickets)
        .reduce((total, tickets) => total + tickets, 0);
    },
    newTickets() {
      return this.ticketsData1
        .filter((ticket) => ticket.status.trim() === "New Tickets")
        .map((ticket) => ticket.tickets)
        .reduce((total, tickets) => total + tickets, 0);
    },
    pendingTickets() {
      return this.ticketsData1
        .filter((ticket) => ticket.status.trim() === "Pending/Queue")
        .map((ticket) => ticket.tickets)
        .reduce((total, tickets) => total + tickets, 0);
    },
    forEvalTickets() {
      return this.ticketsData1
        .filter((ticket) => ticket.status.trim() === "For Eval")
        .map((ticket) => ticket.tickets)
        .reduce((total, tickets) => total + tickets, 0);
    },
    // eslint-disable-next-line vue/return-in-computed-property
    // totalsTickets() {
    //   const tot = []
    //   return this.ticketsData1
    //     .map((ticket) => ticket.tickets)
    //     .reduce((total, tickets) => total + tickets, 0);
    //     this.series
    // },
  },

  async beforeMount() {
    this.loading = true; // Set loading state to true before making API requests

    try {
      const url =
        "https://it-helpdesk-mirdc.ap.ngrok.io/ticketsByCategory?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=38";

      const response = await axios({
        method: "GET",
        url: url,
      });

      console.log("resssss", response.data);
      this.donut = response.data.map((cat) => cat.tickets);
      this.chartOptions1.labels = response.data.map((cat) => cat.category_name);

      console.log(
        "BEEEEEEEEEEFFFOOREEEEEEEEEEEEE",
        response.data.map((cat) => cat.tickets)
      );

      this.series = [
        response.data.reduce((acc, curr) => {
          return acc + curr.tickets;
        }, 0),
      ];

      const url3 =
        "https://it-helpdesk-mirdc.ap.ngrok.io/usersByCategory?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=38";

      const response3 = await axios({
        method: "GET",
        url: url3,
      });
      console.log("test clients", response3.data);
      this.pieClientsCategory = response3.data.map((cat) => cat.clients);
      const categoryNames = response3.data.map((cat) => cat.category_name);
      this.labelClientsCategory.labels = Object.values(categoryNames);
      // this.labelClientsCategory.labels = categoryArr;
      console.log(this.labelClientsCategory.labels);

      console.log(
        "TEST clients fsadfkldsfldsjafklfklasdkj",
        this.labelClientsCategory.labels
      );

      console.log("TESTA");

      // const url3 =
      //   "https://it-helpdesk-mirdc.ap.ngrok.io/usersByCategory?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=38";

      // axios.get(url3).then((response3) => {
      //   const categoryNames = response3.data.map((cat) => cat.category_name);
      //   this.chartOptionbar.xaxis.categories = Object.values(categoryNames);
      // });

      // // console.log("test clients", response3.data);
      // // this.bar.data = response3.data.map((cat) => cat.clients);
      // // const categoryNames = response3.data.map((cat) => cat.category_name);
      // // this.chartOptionbar.xaxis.categories = Object.values(categoryNames);

      // // console.log("chart option bar", this.chartOptionbar);

      // console.log("baaarrr", this.chartOptionbar);
    } catch (error) {
      console.error(error);
    }

    try {
      const url4 =
        "https://it-helpdesk-mirdc.ap.ngrok.io/averageResponseTime?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=1";
      const response4 = await axios.get(url4);
      console.log("qays", response4.data[0].average_response_time);
      this.averageTime = moment(response4.data[0].average_response_time).format(
        "h:mm:ss"
      );
      // const url5 =
      //   "https://it-helpdesk-mirdc.ap.ngrok.io/averageResolutionTimeSimple?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=1";
      // const response5 = await axios.get(url5);
      // console.log("qays", response4.data[0].aaverage_resolution_time_simple);
      // this.averageRESTime = moment(
      //   response5.data[0].aaverage_resolution_time_simple
      // ).format("h:mm:ss");
    } catch (error) {
      console.error(error);
    }

    this.loading = false; // Set loading state to false after data has been loaded
  },

  async mounted() {
    this.ticketsByDivision();

    const url2 =
      "https://it-helpdesk-mirdc.ap.ngrok.io/ticketsByCategory?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=38";

    const response2 = await axios({
      method: "GET",
      url: url2,
    });

    console.log("test clients", response2.data);
    this.donut1 = response2.data.map((cat) => cat.tickets);
    this.chartOptions2.labels = response2.data.map((cat) => cat.category_name);

    console.log("TEST clients erick", this.chartOptions2.labels);

    const urlallClients =
      "https://it-helpdesk-mirdc.ap.ngrok.io/clientsForProj?from=2023%2F01%2F01&to=2023%2F12%2F31&projID=38";

    const responseallClients = await axios({
      method: "GET",
      url: urlallClients,
    });

    console.log("test clients", responseallClients.data);
    this.allClients = responseallClients.data.map((cat) => cat.clients);

    console.log("TEST clientssssssss", this.allClients);
  },
});
</script>

<style media="print" scoped>
@media print {
  .print-media:not(#print-media) {
    margin-top: 50px;
  }

  .print-media2:not(#print-media2) {
    margin-top: 330px;
  }

  .print-media3:not(#print-media3) {
    margin-top: 50px;
  }

  .print-media4:not(#print-media4) {
    margin-top: 330px;
  }

  .print-media5:not(#print-media5) {
    margin-top: 450px;
  }
}

#q-app
  > div
  > div.q-page-container
  > div
  > div.row.flex.flex-center.q-mt-sm
  > div.col-lg-4.col-10.q-mr-md.q-mt-sm.print-media
  > div
  > div
  > div.row
  > div:nth-child(1)
  > label
  > div
  > div
  > div.q-field__control-container.col.relative-position.row.no-wrap.q-anchor--skip
  > div
  .q-field__native
  .text-bold {
  font-weight: 600 !important;
}
</style>
