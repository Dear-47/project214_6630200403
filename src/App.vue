<template>
  <div v-if="font">
    <div class="welcome">
      <p class="title">Welcome to my portfolio</p>
      <div class="wBtn">
        <div class="slide-effect"></div>
        <a class="start" @click="(switchMode = !switchMode), (font = !font)"
          >START</a
        >
      </div>
    </div>
  </div>

  <div v-if="skill">
    <Skill />
  </div>

  <div class="container" v-if="switchMode">
    <nav class="navbar bg-body-tertiary fixed-top">
      <div class="container-fluid">
        <a class="navbar-brand" href="#" v-if="body" style="font-size: 40px"
          >Portfolio</a
        >
        <a class="navbar-brand" href="#" v-if="!body" style="font-size: 40px"
          >My Skills</a
        >
        <div class="ms-auto me-3">
          <button
            type="button"
            v-if="body"
            class="btn btn-danger active"
            style="width: 120px"
            @click="(showDetail = false), (addSubject = false), (editSubject = false)"
          >
            ClearDisplay
          </button>
        </div>
        <div class="me-3">
          <button
            type="button"
            v-if="!body"
            class="btn btn-danger active"
            style="width: 120px"
            @click="(body = !body), (skill = !skill)"
          >
            Go Back
          </button>
        </div>
        <div class="me-3">
          <button
            type="button"
            v-if="body"
            class="btn btn-danger active"
            style="width: 120px"
            @click="(body = !body), (skill = !skill)"
          >
            Skills
          </button>
        </div>

        <button
          v-if="body"
          class="navbar-toggler"
          type="button"
          data-bs-toggle="offcanvas"
          data-bs-target="#offcanvasNavbar"
          aria-controls="offcanvasNavbar"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div
          class="offcanvas offcanvas-end"
          tabindex="-1"
          id="offcanvasNavbar"
          aria-labelledby="offcanvasNavbarLabel"
        >
          <div class="offcanvas-header">
            <h5 class="offcanvas-title" id="offcanvasNavbarLabel">Menu</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="offcanvas"
              aria-label="Close"
            ></button>
          </div>

          <div class="offcanvas-body">
            <ul class="navbar-nav justify-content-end flex-grow-1 pe-3">
              <li class="nav-item">
                <h2>ผลการเรียน</h2>
              </li>
              <li class="nav-item m-2">
                <button
                  type="button"
                  style="width:200px;"
                  class="btn btn-danger active"
                  @click="isShowEditDis = !isShowEditDis"
                >
                  EditDescription
                </button>
              </li>
              <li class="nav-item m-2">
                <button
                  type="button"
                  style="width:200px;"
                  class="btn btn-primary"
                  @click="showDetail = !showDetail"
                >
                  MySubject list!!
                </button>
              </li>
              <li class="nav-item m-2">
                <button
                  class="btn btn-warning"
                  style="width:200px;"
                  @click="addSubject = !addSubject"
                >
                  Add Subject
                </button>
              </li>
              <li class="nav-item m-2">
                <button
                  class="btn btn-success"
                  style="width:200px;"
                  @click="deleteMode = !deleteMode"
                >
                  deleteSubject
                </button>
              </li>
              <li class="nav-item m-2">
                <button
                  class="btn btn-secondary"
                  style="width:200px;"
                  @click="editSubject = !editSubject"
                >
                  Edit Subject
                </button>
              </li>
            </ul>
            <div class="from-delete" v-if="deleteMode">
              <br />
              <br />
              <div
                class="max-w-sm mx-auto mt-10 p-6 bg-white rounded-xl shadow-md"
              >
                <h2>DeleteSubject</h2>
                <form @submit.prevent="submitForm">
                  <div class="mb-4">
                    <label
                      class="block text-sm font-medium mb-1"
                      style="font-size: 20px"
                      >ID of subject :
                    </label>
                    <input
                      type="text"
                      v-model="inputId"
                      style="margin-left: 5px"
                      class="w-full border border-gray-300 p-2 rounded"
                      required
                    />
                  </div>
                  <button type="submit" class="btn btn-warning">Delete</button>
                </form>
              </div>
            </div>
            <div v-if="isShowEditDis">
              <br /><br /><br />
              <EditDes :stdId="this.id" />
            </div>
          </div>
        </div>
      </div>
    </nav>

    <div class="body-part" v-if="body">
      <section id="main" class="container m-5 pt-5 py-5">
        <div class="row">
          <!-- ส่วนรูปภาพ class="shadow-lg rounded"-->
          <div class="col-lg-6 col-md-6 col-sm-12">
            <div class="text-center">
              <div class="flip-box">
                <div class="flip-box-inner">
                  <div class="flip-box-front">
                    <img
                      src="/public/image_nisit.jpg"
                      alt="Nisit"
                      style="width: auto; height: 700px"
                    />
                  </div>
                  <div class="flip-box-back">
                    <img
                      src="/public/image_nisit2.jpg"
                      alt="Nisit"
                      style="width: auto; height: 700px"
                    />
                  </div>
                </div>
              </div>
            </div>
            <br />
            <div v-if="addSubject" style="margin-top: 500px">
              <Addsub />
            </div>
            <div v-if="editSubject" style="margin-top: 500px">
              <Editsub />
            </div>
          </div>

          <!--ส่วนเนื้อหา-->
          <div class="col-lg-6 col-md-6 col-sm-12">
            <div class="display-1" style="color: gray">{{ name }}</div>
            <br />
            <div class="display-6" style="color: gray">ID : {{ id }}</div>
            <br />
            <div class="display-5 text-muted">
              <p class="text-break" style="font-size: 40px; color: gray">
                {{ branch }} from Kasetsart University, Sriracha Campus
              </p>
            </div>
            <br />
            <div class="mt-3 lead text-muted">
              <p class="display-6" style="color: gray">Description</p>
              {{ des }}
            </div>
            <div>
              <br />
              <p style="font-size: 30px; color: gray">
                !! My old school is {{ oldSchool }}.
              </p>
            </div>
            <div>
              <div v-if="showDetail">
                <br /><br /><br />
                <Menu />
              </div>
            </div>
            <br />
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Menu from "./components/Menu.vue";
import Addsub from "./components/Addsub.vue";
import EditDes from "./components/EditDes.vue";
import Skill from "./components/Skill.vue";
import Editsub from "./components/Editsub.vue";

export default {
  name: "App",
  components: {
    Menu,
    EditDes,
    Addsub,
    Skill,
    Editsub,
  },
  data() {
    return {
      name: null,
      wel: null,
      des: null,
      branch: null,
      hobbies: null,
      id: null,
      majorId: null,
      grade: null,
      image: null,
      oldSchool: null,
      showDetail: false,
      isShowEditDis: false,
      addSubject: false,
      switchMode: false,
      font: true,
      skill: false,
      body: true,
      deleteMode: false,
      editSubject: false,

      number_sub: null,
      data_std: [],

      inputId: "", // ค่าในช่องกรอก
      subId: "", // ค่า ID ที่บันทึกไว้จริง
    };
  },

  mounted() {
    fetch(`http://localhost:3000/data_port/`)
      .then((res) => res.json())
      .then((data) => {
        if (Array.isArray(data) && data.length > 0) {
          let data_det = data[0]; // เอาเฉพาะตัวแรกของ array
          this.name = data_det.name;
          this.wel = data_det.wel;
          this.des = data_det.des;
          this.branch = data_det.branch;
          this.hobbies = data_det.hobbies;
          this.id = data_det.id;
          this.majorId = data_det.major_id;
          this.oldSchool = data_det.oldSchool;
        }
      })
      .catch((err) => console.error("Fetch error:", err));
  },
  methods: {
    async delDetail() {
      if (!this.subId) {
        alert("กรุณากรอก ID ของ Subject ที่ต้องการลบ");
        return;
      }

      if (confirm(`ยืนยันลบ Subject ID: ${this.subId} ใช่หรือไม่?`)) {
        try {
          const response = await fetch(
            `http://localhost:3000/subject/${this.subId}`,
            {
              method: "DELETE",
              headers: {
                "Content-Type": "application/json",
              },
            }
          );

          if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
          }

          const result = await response.json();
          alert("ลบข้อมูลสำเร็จ");
          console.log("ผลลัพธ์จากการลบ:", result);

          // รีเซ็ตค่าหลังจากลบสำเร็จ
          this.subId = "";
          this.inputId = "";
          this.deleteMode = false;
        } catch (error) {
          console.error("เกิดข้อผิดพลาดในการลบ:", error);
          alert(`เกิดข้อผิดพลาด: ${error.message}`);
        }
      }
    },
    submitForm() {
      if (!this.inputId) {
        alert("กรุณากรอก ID ของ Subject ที่ต้องการลบ");
        return;
      }
      this.subId = this.inputId;
      this.delDetail();
    },
  },
};
</script>
<style>
.welcome {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: rgb(194, 194, 194);
}

.title {
  font-size: 70px;
  margin-bottom: 230px;
}

.welcome {
  text-align: center;
}

.wBtn {
  border: 8px solid gray;
  border-radius: 15px;
  width: 250px;
  height: auto;
  background-color: none;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  position: absolute;
  overflow: hidden;
  cursor: pointer;
  transition: 0.8s;
}

.btn:hover {
  box-shadow: 11px 13px 20px 9px rgba(0, 0, 0, 0.1);
}

.slide-effect {
  top: 0;
  left: -1400;
  position: absolute;
  width: 300%;
  height: 105%;
  background-color: rgb(68, 68, 68);
  clip-path: polygon(0 0, 94% 0, 100% 100%, 0 100%);
  transition: 0.8s;
}

.start {
  position: relative;
  font-size: 20px;
  color: #ffffff;
  padding: 25px 50px;
  font-family: "Roboto", sans-serif;
  text-transform: uppercase;
  transition: 0.8s;
  letter-spacing: 1px;
}

.btn:hover .start {
  color: #d5d5d5;
  letter-spacing: 0;
}

.flip-box {
  background-color: transparent;
  width: 300px;
  height: 200px;
  border: 1px solid #f1f1f1;
  perspective: 1000px;
}

.flip-box-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-box:hover .flip-box-inner {
  transform: rotateY(180deg);
}

.flip-box-front,
.flip-box-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

.flip-box-front {
  background-color: #bbb;
  color: black;
}

.flip-box-back {
  background-color: dodgerblue;
  color: white;
  transform: rotateY(180deg);
}
</style>
