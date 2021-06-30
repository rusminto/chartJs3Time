<template>
  <div>
    <canvas id="HorizontalChart" width="400" height="400"></canvas>
  </div>
</template>

<script>
import { Chart, registerables } from 'chart.js';
// import 'chartjs-adapter-moment'; // or another adapter to avoid moment
Chart.register(...registerables);
import moment from "moment";
import 'chartjs-adapter-moment';

export default {
  name: 'HorizontalChart',
  mounted(){
    var ctx = document.getElementById('HorizontalChart').getContext('2d');
    var myChart = new Chart(ctx, {
            type: 'bar',
            data: {
            labels: ['Planning (Monthly)', 'Planning (Daily)', 'Actual'],
            datasets: [{
            label: 'Sebango 1',
            backgroundColor: "#D7708C",
            maxBarThickness: 35,
            order: 2,
            data: [
                [moment("2021-06-17 07:00"), moment("2021-06-17 09:00")],
                [moment("2021-06-17 07:00"), moment("2021-06-17 07:30")],
                [moment("2021-06-17 07:00"), moment("2021-06-17 07:20")]
            ],
            pcs: [30, 24, 50]
            }, {
            label: 'Sebango 2',
            backgroundColor: "#707ED7",
            maxBarThickness: 35,
            order: 2,
            data: [
                [moment("2021-06-17 09:00"), moment("2021-06-17 10:30")],
                [moment("2021-06-17 07:30"), moment("2021-06-17 09:20")],
                [moment("2021-06-17 07:20"), moment("2021-06-17 09:10")]
            ],
            pcs: [100, 12, 60]
            }, {
            label: 'Sebango 3',
            maxBarThickness: 35,
            order: 2,
            backgroundColor: "#73D770",
            data: [
                [moment("2021-06-17 10:30"), moment("2021-06-17 13:20")],
                [moment("2021-06-17 09:20"), moment("2021-06-17 10:40")],
                [moment("2021-06-17 09:10"), moment("2021-06-17 10:20")]
            ],
            pcs: [40, 54, 88]
            }, {
            label: 'Sebango 4',
            maxBarThickness: 35,
            order: 2,
            backgroundColor: "#D7A770",
            data: [
                [moment("2021-06-17 13:20"), moment("2021-06-17 15:30")],
                [moment("2021-06-17 10:40"), moment("2021-06-17 11:30")],
                [moment("2021-06-17 10:20"), moment("2021-06-17 10:40")]
            ],
            pcs: [90, 71, 7]
            }, {
            label: 'Sebango 5',
            maxBarThickness: 35,
            order: 1,
            backgroundColor: "#70D7C9",
            data: [
                [moment("2021-06-17 10:50"), moment("2021-06-17 11:20")]
            ],
            pcs: [43]
            }],
        },
        options: {
        indexAxis: 'y',
        plugins: {
          datalabels: {
            color: "#000000",
            align: 'center',
            anchor: 'center',
            formatter: function(value, context) {
              let d = moment(value[1], 'YYYY-MM-DD HH:mm') - moment(value[0], 'YYYY-MM-DD HH:mm');
              var dur = moment.duration(d, 'milliseconds');
              var mins = Math.floor(dur.asMinutes());
              return mins + "'"
              // return value.pcs;
            },
          },
          tooltip: {
          mode: 'point',
          callbacks: {
            label: function({dataIndex, dataset, datasetIndex, raw}) {
                let values = raw
                let pcs = dataset.pcs[dataIndex]
              return moment(values[0]).format('HH:mm') + ' - ' + moment(values[1]).format('HH:mm') + ' = ' + pcs +" pcs"
            }
          }
        }
        },
        legend: {
          display: true
        },
        responsive: true,
        interaction: {
            intersect: false,
        },
        scales: {
          x: {
            type: "time",
            time: {
              unit: "hour",
              parser: "YYYY-MM-DD HH:mm",
              displayFormats: {
                hour: "HH:mm"
              },
            },
            min: moment("2021-06-17 07:00"),
            max: moment("2021-06-17 21:00"),
            stacked: false
          },
          y: {
            stacked: true
          }
        }
      }
    });
  }
}
</script>
