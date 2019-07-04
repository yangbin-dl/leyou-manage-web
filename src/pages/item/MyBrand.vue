<template>
    <div>
      <v-layout class="px-3">
        <v-flex xs2>
          <v-btn color="info" small>新增品牌</v-btn>
        </v-flex>
        <v-spacer/>
        <v-flex xs4>
          <v-text-field label="搜索" hide-deatils append-icon="search" v-model="key"/>
        </v-flex>
      </v-layout>
      <v-data-table
        :headers="headers"
        :items="brands"
        :pagination.sync="pagination"
        :total-items="totalBrands"
        :loading="loading"
        class="elevation-1"
      >
        <template v-slot:items="props">
          <td class="text-xs-center">{{ props.item.id }}</td>
          <td class="text-xs-left">{{ props.item.name }}</td>
          <td class="text-xs-center"><img :src="props.item.image" alt = ""></td>
          <td class="text-xs-left">{{ props.item.letter}}</td>
          <td class="text-xs-center">
            <v-btn flat icon color="info">
              <v-icon>edit</v-icon>
            </v-btn>
            <v-btn flat icon color="error">
              <v-icon>delete</v-icon>
            </v-btn>
          </td>
        </template>
      </v-data-table>
    </div>
</template>

<script>
    export default {
        name: "MyBrand",
      data(){
          return{
            headers:[
              {text: 'id',value: 'id',align: 'center',sortable: true},
              {text: '名称',value: 'name',align: 'center',sortable: true},
              {text: 'LOGO',value: 'image',align: 'center',sortable: false},
              {text: '首字母',value: 'letter',align: 'center',sortable: true},
              {text: '操作',align: 'center',sortable: false},
            ],
            brands:[],
            pagination: {},
            totalBrands: 0,
            loading: false,
            key:"",
          }
      },
      created() {
          this.brands = [
            {
              "id": 2032,
              "name": "OPPO",
              "image": "http://img10.360buyimg.com/popshop/jfs/t2119/133/2264148064/4303/b8ab3755/56b2f385N8e4eb051.jpg",
              "letter": "O"
            },
            {
              "id": 2033,
              "name": "飞利浦（PHILIPS）",
              "image": "http://img12.360buyimg.com/popshop/jfs/t18361/122/1318410299/1870/36fe70c9/5ac43a4dNa44a0ce0.jpg",
              "letter": "F"
            },
            {
              "id": 2034,
              "name": "华为（HUAWEI）",
              "image": "http://img10.360buyimg.com/popshop/jfs/t5662/36/8888655583/7806/1c629c01/598033b4Nd6055897.jpg",
              "letter": "H"
            },
            {
              "id": 2036,
              "name": "酷派（Coolpad）",
              "image": "http://img10.360buyimg.com/popshop/jfs/t2521/347/883897149/3732/91c917ec/5670cf96Ncffa2ae6.jpg",
              "letter": "K"
            },
            {
              "id": 2037,
              "name": "魅族（MEIZU）",
              "image": "http://img13.360buyimg.com/popshop/jfs/t3511/131/31887105/4943/48f83fa9/57fdf4b8N6e95624d.jpg",
              "letter": "M"
            }
          ];
          this.totalBrands = 15;
          this.loadBrands();
      },
      watch: {
          key(){
            this.loadBrands();
          },
        pagination:{
            deep: true,
            handler(){
              this.loadBrands();
            }
        }
      },
      methods: {
        loadBrands(){
          this.$http.get("/brand/page",{
            params:{
              page: this.pagination.page,
              rows: this.pagination.rowsPerPage,
              sortBy: this.pagination.sortBy,
              desc: this.pagination.descending,
              key: this.key

            }
          })
        }
      }
    }
</script>

<style scoped>

</style>
