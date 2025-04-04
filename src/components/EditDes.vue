<template>
  <div class="card" style="background-color: #fffdf0">
    <div class="card-body">
          <form @submit.prevent="handleSubmit">
            <label for="stdID" class="form-label">Edit name</label>
            <input
              type="text"
              id="name"
              class="form-control"
              v-model.trim="des.name"
            />
            <br/>
            <label for="student_id" class="form-label">Edit ID</label>
            <input
              type="text"
              id="student_id"
              class="form-control"
              v-model.trim="des.id"
            />
            <br/>
            <label for="branch" class="form-label">Edit branch</label>
            <input
              type="text"
              id="branch"
              class="form-control"
              v-model.trim="des.branch"
            />
            <br/>
            <label for="des" class="form-label">Edit description</label>
            <input
              type="text"
              id="des"
              class="form-control"
              v-model.trim="des.des"
            />
            <br/>
            <label for="oldSchool" class="form-label">Edit oldSchool</label>
            <input
              type="text"
              id="oldSchool"
              class="form-control"
              v-model.trim="des.oldSchool"
            />
          <div class="col-2 mt-4 align-items-center">
            <button type="submit" class="btn btn-warning">บันทึก</button>
          </div>
        </form>
        <div class="alert alert-success" v-if="addOk">
          {{ addMessage }}
        </div>
        <div class="alert alert-danger" v-if="addErr">
          {{ addMessage }}
        </div>
    </div>
  </div>
</template>

<script>

import { EventBus } from '@/event-bus';

export default {
  name:"EditDes",
  props: ['stdId'],
  data() {
    return {
      des: {
        name: null,
        id: null,
        branch: null,
        des: null,
        oldSchool: null,
      },
      addErr: null,
      addOk: null,
      addMessage: null
    }
  },
  methods: {
    handleSubmit() {
      fetch(`http://localhost:3000/data_port/${this.stdId}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.des),
      })
        .then(() => {
          this.addOK = true;
          this.addErr = false;
          this.addMessage = "แก้ไขข้อมูลสำเร็จ";
          EventBus.emit("stdChange",{message:"add"});
        })
        .catch((err) => {
          this.addErr = true;
          this.addOK = false;
          this.addMessage = err;
        });
    },
  }  
}  
</script>

<style>

</style>