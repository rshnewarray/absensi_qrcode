<template>
    <div id="home">

        <!-- breadcrumb -->
            <nav class="text-sm font-semibold mb-6" aria-label="Breadcrumb">
              <ol class="list-none p-0 inline-flex">
                <li class="flex items-center text-blue-500">
                  <a href="#" class="text-gray-700">Home</a>
                  <svg class="fill-current w-3 h-3 mx-3" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><path d="M285.476 272.971L91.132 467.314c-9.373 9.373-24.569 9.373-33.941 0l-22.667-22.667c-9.357-9.357-9.375-24.522-.04-33.901L188.505 256 34.484 101.255c-9.335-9.379-9.317-24.544.04-33.901l22.667-22.667c9.373-9.373 24.569-9.373 33.941 0L285.475 239.03c9.373 9.372 9.373 24.568.001 33.941z"/></svg>
                </li>
                <li class="flex items-center">
                  <a href="#" class="text-gray-600">Dashboard</a>
                </li>
              </ol>
            </nav>
            <!-- breadcrumb end -->

            <div class="lg:flex justify-between items-center mb-6">
              <p class="text-2xl font-semibold mb-2 lg:mb-0">Selamat Datang {{namaUser}}!</p>
              <!-- <button class="bg-blue-500 hover:bg-blue-600 focus:outline-none rounded-lg px-6 py-2 text-white font-semibold shadow">View Logs</button> -->
            </div>

    </div>
</template>

<script>
import Chart from 'chart.js';
import axios from 'axios';

export default {
    name: 'DashboardHome',
    data() {
        return {
          namaUser: '',
        }
    },
    methods: {
      getData: function(){
        if (JSON.parse(localStorage.item).level == 2) {
          this.$axios
            .post(this.$store.state.url.BASE_API + `/showmahasiswa`, {
              id_user: JSON.parse(localStorage.item).id_user
            }, {
            headers: {
              'Content-type': 'application/x-www-form-urlencoded',
            },
          })
          .then((data) => {
            console.log(data);
            this.namaUser = data.data[0].nama
          }).catch(err => {
            console.error(err);
          });
        } else {
          this.$axios
            .post(this.$store.state.url.BASE_API + `/showdosen`, {
              id_user: JSON.parse(localStorage.item).id_user
            }, {
            headers: {
              'Content-type': 'application/x-www-form-urlencoded',
            },
          })
          .then((data) => {
            console.log(data);
            this.namaUser = data.data[0].nama
          }).catch(err => {
            console.error(err);
          });
        }
      }
    },
    mounted () {
    }
}
</script>