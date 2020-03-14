<template>
  <div class="container">
    <div class="mb-20">
      <div class="mt-10">
        <div class="text-center">
          <p>基础列表</p>
        </div>
        <!-- data border show-header stripe height max-height @click-column @click-row @click-header-->
        <n-table :data="tableData" :border="true" :stripe="true">
          <n-table-column lable="第一列" prop="a"> </n-table-column>
          <n-table-column lable="第二列" prop="b"></n-table-column>
          <n-table-column lable="第三列" prop="c"></n-table-column>
          <template slot="footer">
            <span @click="isShow = true">show Dialog</span>
          </template>
        </n-table>
      </div>
    </div>
    <n-dialog :visible.sync="isShow" width="30%" height="400px">
      <template slot="title">新世纪哦发家史</template>
      <n-table :data="tableData" :border="true" :stripe="true">
        <n-table-column lable="第一列" prop="a"> </n-table-column>
        <n-table-column lable="第二列" prop="b"></n-table-column>
        <n-table-column lable="第三列" prop="c"></n-table-column>
        <template slot="footer">
          footer
        </template>
      </n-table>
    </n-dialog>
  </div>
</template>

<script>
import NButton from "~/components/NButton";
import NIcon from "~/components/NIcon";
import NTable from "~/components/NTable";
import NTableColumn from "~/components/NTableColumn";
import Logo from "~/components/Logo.vue";
import NDialog from "~/components/NDialog";

export default {
  components: {
    Logo,
    NButton,
    NTable,
    NTableColumn,
    NIcon,
    NDialog
  },
  data() {
    return {
      tableData: [
        { a: 1, b: 2, c: 3 },
        { a: 2, b: 3, c: 4 },
        { a: 3, b: 4, c: 5 },
        { a: 2, b: 3, c: 4 },
        { a: 3, b: 4, c: 5 }
      ],
      isShow: false,
      text: {
        value: null,
        disabled: null,
        id: "text-field",
        name: "text-field"
      }
    };
  },
  mounted() {},
  methods: {
    newChange(val) {
      console.log(val);
    }
  }
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
