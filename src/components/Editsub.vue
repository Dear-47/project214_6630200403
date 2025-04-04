<template>
    <div>
    <p style="font-size: 40px;">
      Edit Subject 
    </p>
  </div>
  <div class="card" style="background-color: #fffdf0">
    <div class="card-body">
      <form @submit.prevent="handleSubmit">
        <div class="row">
            <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
                <label for="id" class="form-label">รหัสวิชาที่ต้องการเปลี่ยน</label>
                <input
                type="text"
                id="Eid"
                class="form-control"
                v-model.trim="sub.eid"
                />
            </div>
          <div class="col-lg-8 col-md-8 col-sm-6 mt-2">
            <label for="name" class="form-label">ชื่อวิชา</label>
            <input
              type="text"
              id="subName"
              class="form-control"
              v-model.trim="sub.name"
            />
          </div>
          <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
            <label for="grade" class="form-label">grade</label>
              <input
                type="text"
                id="grade"
                class="form-control"
                v-model.trim="sub.grade"
              />
          </div>
          <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
            <label for="credit" class="form-label">credit</label>
              <input
                type="text"
                id="credit"
                class="form-control"
                v-model.trim="sub.credit"
              />
          </div>
        </div>
        <div class="col-2 mt-4 align-items-center">
            <button type="submit" class="btn btn-warning">บันทึก</button>
          </div>
      </form>
      <div class="alert alert-success" v-if="addOK">
          {{ addMessage }}
        </div>
        <div class="alert alert-danger" v-if="addError">
          {{ addMessage }}
        </div>
    </div>
  </div>
</template>

<script>
import {EventBus} from "../event-bus"

export default {
    name: "Editsub",
    data(){
        return{
            sub:{
                eid: null,
                id: null,
                name: null,
                grade: null,
                credit: null,
            },
            addOK: false,
            addError: false,
            addMessage: null,
        }
    },
    methods: {
  handleSubmit() {
    if (!this.sub.eid) {
      this.addError = true;
      this.addOK = false;
      this.addMessage = "กรุณากรอกรหัสวิชาที่ต้องการแก้ไข";
      return;
    }

    let subject = {
      id: this.sub.id,
      name: this.sub.name,
      grade: this.sub.grade,
      credit: this.sub.credit,
    };

    fetch(`http://localhost:3000/subject/${this.sub.eid}`, {
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(subject), 
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(() => {
      this.addOK = true;
      this.addError = false;
      this.addMessage = "แก้ไขข้อมูลสำเร็จ";
      EventBus.emit("stdChange", { message: "edit" });
      this.resetForm();
    })
    .catch((err) => {
      this.addError = true;
      this.addOK = false;
      this.addMessage = "เกิดข้อผิดพลาด: " + err.message;
    });
  },
  resetForm() {
    this.sub = {
      eid: null,
      id: null,
      name: null,
      grade: null,
      credit: null,
    };
  }
},
}
</script>

<style>

</style>