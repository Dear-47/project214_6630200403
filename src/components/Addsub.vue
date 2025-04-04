<template>
  <div>
    <p style="font-size: 40px">Add Subject</p>
  </div>
  <div class="card" style="background-color: #fffdf0">
    <div class="card-body">
      <form @submit.prevent="handleSubmit">
        <div class="row">
          <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
            <label for="id" class="form-label">รหัสวิชา</label>
            <input
              type="text"
              id="id"
              class="form-control"
              v-model.trim="sub.id"
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
import { EventBus } from "../event-bus";

export default {
  name: "Addsub",
  data() {
    return {
      sub: {
        id: null,
        name: null,
        grade: null,
        credit: null,
      },
      addOK: false,
      addError: false,
      addMessage: null,
    };
  },
  methods: {
    handleSubmit() {
      let subject = {
        id: this.sub.id,
        name: this.sub.name,
        grade: this.sub.grade,
        credit: this.sub.credit,
      };
      fetch(`http://localhost:3000/subject`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(subject),
      })
        .then(() => {
          this.addOK = true;
          this.addErr = false;
          this.addMessage = "เพิ่มข้อมูลสำเร็จ";
          EventBus.emit("stdChange", { message: "add" });
        })
        .catch((err) => {
          this.addErr = true;
          this.addOK = false;
          this.addMessage = err;
        });
    },
  },
};
</script>

<style></style>
