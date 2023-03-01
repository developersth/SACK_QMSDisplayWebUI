<template>
  <div>
    <table class="table table-striped table-bordered" style="width: 100%">
      <thead class="thead-dark">
        <th class="text-center" style="width:10%">
          <v-btn block>#</v-btn>
        </th>
        <th style="width: 10%" class="text-center" v-for="(item, index) in itemsBay" :key="index">
          <v-btn block size="lg" dark :color="getActiveQueue(item.is_queue)">{{ item.bay_name }}</v-btn>
        </th>
        <th class="text-center" style="width: 10%">
          <v-btn block size="lg" color="primary">รับตั๋ว</v-btn>
        </th>
      </thead>
      <tbody>
        <td>
          <div class="text-center">
            <v-btn block>
              Loading
            </v-btn>
          </div>
        </td>
        <td v-for="(item, index) in itemsLoad" :key="index">
          <v-card color="#385F73" dark v-if="item.is_active">
            <v-card-title class="text-h5">
              {{ item.truck_id }}
            </v-card-title>

            <v-card-subtitle>{{ item.driver_name }}</v-card-subtitle>

            <v-card-actions>
              <v-btn block variant="text">
                {{ item.status }}
              </v-btn>
            </v-card-actions>
          </v-card>
        </td>

        <td></td>
        <tr>
          <td rowspan="3">
            <v-btn block>Standby</v-btn>
          </td>
        </tr>
        <tr>
          <td v-for="(item, index) in itemsBay" :key="index">
            <div v-for="(itemBay, idxItemBay) in loadItemStandBy(item.bay_no)" :key="idxItemBay">
              <v-card color="#1F7087" dark  class="mt-2">
                <v-card-title class="text-h5">
                  {{ itemBay.truck_id }}
                </v-card-title>
                <v-card-subtitle>{{ itemBay.driver_name }}</v-card-subtitle>

                <v-card-actions>
                  <v-btn block dark :color="getCallQueue(itemBay.call_queue)">
                    {{ itemBay.status }}
                  </v-btn>
                </v-card-actions>
              </v-card>
              
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      itemsBay: [
        { bay_no: 1, bay_name: 'BAY 1', is_queue: true },
        { bay_no: 2, bay_name: 'BAY 2', is_queue: false },
        { bay_no: 3, bay_name: 'BAY 3', is_queue: true },
        { bay_no: 4, bay_name: 'BAY 4', is_queue: false },
        { bay_no: 5, bay_name: 'BAY 5', is_queue: true },
        { bay_no: 6, bay_name: 'BAY 6', is_queue: true },
        { bay_no: 7, bay_name: 'BAY 7', is_queue: true },
      ],
      itemsLoad: [
        {
          load_no: 1,
          truck_id: '75-0001',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายชวลิต อรุณไพร',
        },
        {
          load_no: 2,
          truck_id: '75-0002',
          is_active: false,
          status: 'กำลังเติม',
          driver_name: 'นายนิพล โพสฤทธ',
        },
        {
          load_no: 3,
          truck_id: '75-0003',
          is_active: true,
          status: 'เติมเสร็จ',
          driver_name: 'นายสวง สาระศาลิน',
        },
        {
          load_no: 4,
          truck_id: '75-0004',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายสมบัติ นามฝาง',
        },
        {
          load_no: 5,
          truck_id: '75-0005',
          is_active: false,
          status: 'เติมเสร็จ',
          driver_name: 'นายปรีชา  คเณรุพันธ์',
        },
        {
          load_no: 6,
          truck_id: '75-0006',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายชวลิต อรุณไพร',
        },
        {
          load_no: 7,
          truck_id: '75-0007',
          is_active: true,
          status: 'เติมเสร็จ',
          driver_name: 'นายศุภกรณ์ชัย ศรลัมภ์',
        },
      ],
      itemsStandby: [
        {
          bay_no: 1,
          load_no: 1,
          truck_id: '75-0001',
          is_active: true,
          status: 'เรียกเข้าเติม',
          driver_name: 'นายชวลิต',
          call_queue: true,
        },
        {
          bay_no: 1,
          load_no: 2,
          truck_id: '75-0002',
          is_active: false,
          status: 'รอเข้าเติม',
          driver_name: 'นายนิพล',
          call_queue: false,
        },
        {
          bay_no: 1,
          truck_id: '75-0003',
          is_active: true,
          status: 'รอเข้าเติม',
          driver_name: 'นายสวง',
          call_queue: false,
        },
        {
          bay_no: 3,
          load_no: 4,
          truck_id: '75-0004',
          is_active: true,
          status: 'รอเข้าเติม',
          driver_name: 'นายสมบัติ',
          call_queue: false,
        },
        {
          bay_no: 3,
          load_no: 5,
          truck_id: '75-0005',
          is_active: false,
          status: 'รอเข้าเติม',
          driver_name: 'นายปรีชา',
          call_queue: false,
        },
        {
          bay_no: 7,
          load_no: 6,
          truck_id: '75-0006',
          is_active: true,
          status: 'รอเข้าเติม',
          driver_name: 'นายชวลิต',
          call_queue: false,
        },
        {
          bay_no: 7,
          load_no: 7,
          truck_id: '75-0007',
          is_active: true,
          status: 'เรียกเข้าเติม',
          driver_name: 'นายศุภกรณ์ชัย สิริวัฒนพาณิชย์รักภักดี',
          call_queue: false,
        },
      ],
    }
  },
  methods: {
    getActiveQueue(is_queue) {
      return is_queue ? 'green' : 'red'
    },
    getCallQueue(active) {
      return active ? 'green' : 'warning'
    },
    loadItemStandBy(bay_no) {
      const check = this.itemsStandby.filter((item) => item.bay_no === bay_no)
      if (check) {
        return this.itemsStandby.filter((item) => item.bay_no === bay_no)
      } else {
        return null
      }
    },
  }
}
</script>

