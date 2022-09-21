  <template>
    <div class="app">
      <InputVal
        :listArray="cityList"
      />
    </div>
  </template>
  <script>
    import InputVal from "./components/InputVal.vue";
    import axios from "axios";
    export default {
      name: "App",
      components: {
        InputVal,
      },
      data() {
        return {
          cityList: [],
        };
      },
      methods: {
        async fetchCityApi() {
          try {
            await axios
              .get("https://provinces.open-api.vn/api/")
              .then((res) => (this.cityList = [...res.data]));
          } catch (e) {
            console.log("Failed to fetch data");
          }
        },
      },
      created() {
        this.fetchCityApi();
      },
    };
    </script>
  <style lang="scss">
  * {
    margin: 0;
    box-sizing: border-box;
  }
  .app {
    margin-top: 140px;
    text-align: center;
  }
  </style>