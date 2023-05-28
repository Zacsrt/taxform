<template>
  <div class="grid">
    <div class="formheader">
      <div class="header">
        <input
          type="radio"
          value="ผู้หัก ณ ที่จ่าย"
          v-model="taxdata.firstchoice"
        />
        <label for="tax-firstchoice">ผู้หัก ณ ที่จ่าย</label>
        <input type="radio" value="กระทำการแทน" v-model="taxdata.firstchoice" />
        <label for="tax-firsthoice">กระทำการแทน</label>
      </div>
        <div class="header-right">
        เลขที่เอกสาร: WTNXXXYYMM/####
      </div>
      
    </div>



    <div class="formuser">
      <div class="pink">
      <div class="pink1">
      <label for="tax-user">ผู้มีหน้าที่หักภาษี ณ ที่จ่าย</label><br/>
      <input
        type="text"
        placeholder="Code หรือ Name"
        v-model.trim="taxdata.username"
      />
    </div>
    <div class="pink2">
      <label for="tax-usernum">เลขประจำตัวผู้เสียภาษีอากร</label><br/>
      <input
        type="number"
        placeholder="เลขประจำตัวผู้เสียภาษีอากร"
        v-model="taxdata.usernum"
      />
    </div>
  </div>
    <div class="pink3">
      <br/><label for="tax-useraddress">ที่อยู่ :</label>
      <input type="text" v-model.trim="taxdata.useraddress" />
    </div>
  </div>

    <div class="formagent">
      <div class="orange">
        <div class="orange1">
      <label for="tax-agent">กระทำการแทนโดย</label><br/>
      <input
        type="text"
        placeholder="Code หรือ Name"
        v-model.trim="taxdata.agentname"
      />
    </div>
    <div class="orange2">
      <label for="tax-agentnum">เลขประจำตัวผู้เสียภาษีอากร</label><br/>
      <input
        type="number"
        placeholder="เลขประจำตัวผู้เสียภาษีอากร"
        v-model="taxdata.agentnum"
      />
    </div>
    </div>
    <div class="orange3">
      <br/><label for="tax-agentaddress">ที่อยู่ :</label>
      <input type="text" v-model.trim="taxdata.agentaddress" />
    </div>
  </div>

    <div class="formcustomer">
      <div class="yellow">
        <div class="yellow1">
      <label for="tax-customer">ผู้ถูกหักภาษี ณ ที่จ่าย</label><br/>
      <input
        type="text"
        placeholder="Code หรือ Name"
        v-model.trim="taxdata.cusname"
      />
    </div>
    <div class="yellow2">
      <label for="tax-cusnum">เลขประจำตัวผู้เสียภาษีอากร</label><br/>
      <input
        type="number"
        placeholder="เลขประจำตัวผู้เสียภาษีอากร"
        v-model="taxdata.cusnum"
      />
    </div>
    </div>
    <div class="yellow3">
      <br/><label for="tax-cusaddress">ที่อยู่ :</label>
      <input type="text" v-model.trim="taxdata.cusaddress" />
    </div><br/><br/><br/><br/><br/>
      <hr />

      <div class="yellow4">
      <label for="tax-order">ลำดับ :</label>
      <input type="number" placeholder="number" v-model="taxdata.cusorder" />
      <input type="radio" value="ภ.ง.ด 3" v-model="taxdata.cuschoice" />
      <label for="tax-cuschoice">ภ.ง.ด 3</label>
      <input type="radio" value="ภ.ง.ด 53" v-model="taxdata.cuschoice" />
      <label for="tax-cuschoice">ภ.ง.ด 53</label>
    </div>
    <div class="yellow5">
      <input
        type="checkbox"
        value="ส่งเอกสารให้กรมสรรพากร"
        v-model="taxdata.cuscheck"
      />
      <label for="tax-check">ส่งเอกสารให้กรมสรรพากร</label>
    </div>
    <div class="yellow6">
      <br /> <label for="tax-cusdate">วันที่ออกเอกสาร :</label>
      <div class="yellow7">
      <VueDatePicker
        v-model="taxdata.date"
        :enable-time-picker="false"
        model-type="dd.MM.yyyy"
        placeholder="DD-MM-YYYY"
      />
    </div>
    </div>
    </div>

    <div class="formtable">
      <table>
        <tr>
          <th>ลำดับ</th>
          <th>ประเภทเงินได้</th>
          <th>(%)</th>
          <th>จำนวนเงินที่จ่าย</th>
          <th>ภาษีที่หักและนำส่งไว้</th>
          <th>การดำเนินการ</th>
        </tr>
        <tr v-for="index in 4" :key="index">
          <td>{{ index }}</td>
          <template v-if="index === 1">
            <td>เงินเดือน ค่าจ้าง เบี้ยเลี้ยง โบนัส ฯลฯ</td>
          </template>
          <template v-else-if="index === 2">
            <td>ค่าธรรมเนียมค่านายหน้า ฯลฯ</td>
          </template>
          <template v-else-if="index === 3">
            <td>ค่าแห่งสิทธิ์ ฯลฯ</td>
          </template>
          <template v-else-if="index === 4">
            <td>ค่าดอกเบี้ย ฯลฯ</td>
          </template>
          <template v-else>
            <td></td>
          </template>
          <td><input type="number" v-model="cal.percal[index]" /></td>
          <td><input type="number" v-model="cal.loss[index]" /></td>
          <td>{{ calculatedResult(index) }}</td>
          <td><i class="material-icons">hourglass_bottom</i></td>
        </tr>
      </table>
    </div>

    <div class="formbutton">
      <button @click="sentdata">Save</button>
      <button @click="resetdata">Cancel</button>
    </div>
  </div>
</template>
  
  <script>
import axios from "axios";
import VueDatePicker from "@vuepic/vue-datepicker";
import "@vuepic/vue-datepicker/dist/main.css";
export default {
  name: "TaxForm",
  components: {
    VueDatePicker,
  },
  data() {
    return {
      taxdata: {
        firstchoice: "",
        username: "",
        usernum: "",
        useraddress: "",
        agentname: "",
        agentnum: "",
        agentaddress: "",
        cusname: "",
        cusnum: "",
        cusaddress: "",
        cusorder: "",
        cuschoice: "",
        cuscheck: "",
        date: null,
        percent: "",
      },
      cal: {
        percal: {},
        loss: {},
      },
    };
  },
  methods: {
    async sentdata() {
      console.log(this.taxdata);
      const result = await axios.post("http://localhost:3000/taxdata", {
        firstchoice: this.taxdata.firstchoice,
        username: this.taxdata.username,
        usernum: this.taxdata.usernum,
        useraddress: this.taxdata.useraddress,
        agentname: this.taxdata.agentname,
        agentnum: this.taxdata.agentnum,
        agentaddress: this.taxdata.agentaddress,
        cusname: this.taxdata.cusname,
        cusnum: this.taxdata.cusnum,
        cusaddress: this.taxdata.cusaddress,
        cusorder: this.taxdata.cusorder,
        cuschoice: this.taxdata.cuschoice,
        cuscheck: this.taxdata.cuscheck,
        date: this.taxdata.date,
        percent: this.taxdata.percent,
      });
      console.log("result", result);
      location.reload();
    },

    calculatedResult(index) {
      let percalValue = this.cal.percal[index];
      let lossValue = this.cal.loss[index];
      if (percalValue && lossValue) {
        let result = (percalValue / 100) * lossValue;
        this.taxdata.percent = {
          ...this.taxdata.percent,
          [index]: result.toFixed(2),
        };
        return result;
      }
      this.taxdata.percent = { ...this.taxdata.percent, [index]: null };
      return null;
    },
    resetdata() {
      this.taxdata.firstchoice = "";
      this.taxdata.username = "";
      this.taxdata.usernum = "";
      this.taxdata.useraddress = "";
      this.taxdata.agentname = "";
      this.taxdata.agentnum = "";
      this.taxdata.agentaddress = "";
      this.taxdata.cusname = "";
      this.taxdata.cusnum = "";
      this.taxdata.cusaddress = "";
      this.taxdata.cusorder = "";
      this.taxdata.cuschoice = "";
      this.taxdata.cuscheck = "";
      this.taxdata.date = null;
      this.taxdata.percent = "";
      this.cal.percal = {};
      this.cal.loss = {};
    },
  },
};
</script>
  
  <style scoped>
@import './styles.css';
@import './responsive.css';
</style>