<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";

const data = ref(null);

const fetchData = () => {
  axios
    .get("https://test-api-py77dwlbxa-df.a.run.app/data")
    .then((response) => {
      data.value = response.data;
      console.log(response.data);
    })
    .catch((error) => {
      console.log(error);
    });
};

onMounted(() => {
  fetchData();
});
</script>
<template>
  <div class="card">
    <div class="card-header pb-0">
      <h6>รายการขอขึ้นทะเบียน</h6>
    </div>
    <div class="card-body px-0 pt-0 pb-2">
      <div class="table-responsive p-0">
        <table class="table align-items-center mb-0">
          <thead>
            <tr>
              <th
                class="text-uppercase text-secondary text-xs font-weight-bolder opacity-7"
              >
                ชื่อหน่วยงาน
              </th>
              <th
                class="text-uppercase text-secondary text-xs font-weight-bolder opacity-7 ps-2"
              >
                รหัสหน่วยงาน
              </th>
              <th
                class="text-center text-uppercase text-secondary text-xs font-weight-bolder opacity-7"
              >
                วันที่ขึ้นทะเบียน
              </th>
              <th
                class="text-center text-uppercase text-secondary text-xs font-weight-bolder opacity-7"
              >
                ชื่อผู้ตรวจสอบ
              </th>
              <th
                class="text-center text-uppercase text-secondary text-xs font-weight-bolder opacity-7"
              >
                วันที่ตรวจสอบ
              </th>
              <th
                class="text-center text-uppercase text-secondary text-xs font-weight-bolder opacity-7"
              >
                สถานะ
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in data" :key="index">
              <td>
                <div class="d-flex px-2 py-1">
                  <div class="d-flex flex-column justify-content-center">
                    <h6 class="mb-0 text-xs">{{ item.name }}</h6>
                  </div>
                </div>
              </td>
              <td>
                <p class="text-xs font-weight-bold mb-0">{{ item.code }}</p>
              </td>
              <td class="align-middle text-center text-sm">
                <span class="text-secondary text-xs font-weight-bold">{{
                  item.createDate
                }}</span>
              </td>
              <td class="align-middle text-center">
                <span class="text-secondary text-xs font-weight-bold">
                  {{ item.verifyBy }}
                </span>
              </td>
              <td class="align-middle text-center text-sm">
                <span class="text-secondary text-xs font-weight-bold">{{
                  item.verifyDate
                }}</span>
              </td>
              <td class="align-middle text-center text-sm">
                <span
                  v-if="item.status === 'รอตรวจสอบ'"
                  class="badge badge-md bg-gradient-info"
                  >{{ item.status }}</span
                >
                <span
                  v-if="item.status === 'พิจารณาเอกสาร'"
                  class="badge badge-md bg-gradient-warning"
                  >{{ item.status }}</span
                >
                <span
                  v-if="item.status === 'ขึ้นทะเบียน'"
                  class="badge badge-md bg-gradient-secondary"
                  >{{ item.status }}</span
                >
                <span
                  v-if="item.status === 'ออกเอกสาร'"
                  class="badge badge-md bg-gradient-success"
                  >{{ item.status }}</span
                >
                <span
                  v-if="item.status === 'แก้ไข ครั้งที่ 1.1'"
                  class="badge badge-md bg-gradient-primary"
                  >{{ item.status }}</span
                >
                <span
                  v-if="item.status === 'แก้ไข ครั้งที่ 1.2'"
                  class="badge badge-md bg-gradient-light"
                  >{{ item.status }}</span
                >
                <span
                  v-if="item.status === 'ตอบกลับการแก้ไข 1.1'"
                  class="badge badge-md bg-gradient-dark"
                  >{{ item.status }}</span
                >
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
