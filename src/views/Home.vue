<template>
  <div class="container">
    <!-- Start Header -->
    <div class="row mt-4 mb-5">
        <div class="col-md-2 pl-0" v-for="item in box" :key="item.name">
            <img :src="item.img" :alt="item.name" class="img-fluid shadow rounded" :rounded="true">
            <p class="text-muted text-uppercase text-center small mt-2 font-weight-bold">{{ item.name }}</p>
        </div>
    </div>
    <!-- End Header -->

    <div class="col-md-10 offset-md-1">
      <p class="text-left mb-0 font-weight-bold h5" style="color: #004000">TOP 10 HITS</p>
      <table outlined style="width: 100%;">
        <tr v-for="item in table" :key="item.id">
          <td class="text-center display-4 text-muted" style="width: 10%;">{{item.id}}</td>

          <td class="text-muted text-uppercase text-left" style="width: 50%;"><br>
              <p class="pr-0 font-weight-bold">{{item.Title}}</p>
              <p style="font-size:x-small; margin-top: -20px;">{{item.name}}</p>
              <p style="font-size:small; margin-top: -25px;">__</p>
          </td>

          <td class="text-muted text-uppercase text-center" style="width: 10%;"><br>
              <p class="pr-0 h4" style="font-weight: bolder;">{{item.votes}}</p>
              <p style="margin-top: -15px; font-weight: bold; font-size: x-small;">votes</p>
          </td>

          <td class="text-muted text-uppercase text-center" style="width: 15%;">
            <div class="h3 mb-0 text-muted">
              <button class="btn btn-text mr-1" @click.prevent="increment(item)">
                <b-icon icon="triangle-fill" style="color: #6c757d;"></b-icon><br>
                <p style="font-size:xx-small; margin-bottom: 0px">UP</p>
              </button>
              <button class="btn mr-1" @click.prevent="decrement(item)">
                <b-icon icon="triangle-fill" style="color: #6c757d;" flip-v></b-icon>
                <p style="font-size:xx-small; margin-bottom: 0px">DOWN</p>
              </button>
            </div>
          </td>
          <td style="width: 10%;">
              <img :src="item.img" :alt="item.title" style="width: 100px; height: auto;" class="img-fluid round">
          </td>
        </tr>
      </table>
    </div> 
  </div>
</template>

<script>
  export default {
    data() {
      return {
        box: [
              { img: 'https://www.joox.co.za/wp-content/uploads/2019/04/1000x1000-playlist-and-facebook-800x800.jpg', name: 'avicii' },
              { img: 'https://f4.bcbits.com/img/a2889856732_10.jpg', name: 'mosaic' },
              { img: 'https://images.hhv.de/catalog/shop_detail_zoom/00173/173658.jpg', name: 'bob marley' },
              { img: 'https://static.fnac-static.com/multimedia/Images/FR/NR/41/e6/ac/11331137/1540-1/tsp20190808110045/West-End.jpg', name: '69 eyes' },
              { img: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRJehCJMu8oBX9ysWG6WrV4dcPF310jFGHAFqTXrh7XMQ6ZbWuMMA&s', name: 'angie' },
              { img: 'data:image/jpeg;base64,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', name: 'monster' },
            ],
            table: [
              { id: 1, Title: 'MAMBISA', name:'MAZ BAZAR', votes: 59, img: 'https://images.hhv.de/catalog/shop_detail_zoom/00173/173658.jpg' },
              { id: 2, Title: 'BARABAS', name:'RITX', votes: 58, img: 'https://images.hhv.de/catalog/shop_detail_zoom/00173/173658.jpg' },
              { id: 3, Title: 'STARBOY', name:'THEWEEKND', votes: 38, img: 'https://images.hhv.de/catalog/shop_detail_zoom/00173/173658.jpg' },
              { id: 4, Title: 'NEVERLAND', name:'IRIS', votes: 3, img: 'https://images.hhv.de/catalog/shop_detail_zoom/00173/173658.jpg' },
              { id: 5, Title: 'NO WOMAN NO CRY', name:'BOB MARLEY', votes: 1, img: 'https://images.hhv.de/catalog/shop_detail_zoom/00173/173658.jpg' },
            ]
      }
    },
    methods: {
      increment (item) {
        item.votes += 1
      },
      decrement (item) {
        if (item.votes > 0) {
          item.votes -= 1 
        }
      }
    }
  }
</script>
<style>
  table, tr{
    border: 1px solid #6c757d;
  }
</style>
