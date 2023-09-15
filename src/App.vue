<script setup>
import { ref,computed  } from 'vue';
const list_local = ref([


]);



function list_local_control(name, quantity) {
  const existingItemIndex = list_local.value.findIndex(item => item.name === name);

  if (existingItemIndex !== -1) {
    list_local.value[existingItemIndex].quantity += quantity;
    list_local.value[existingItemIndex].price = list_local.value[existingItemIndex].quantity * travelList.value.find(item => item.name === name).price;
  } else {
    const item = {
      name: name,
      quantity: quantity,
      price: quantity * travelList.value.find(item => item.name === name).price
    };
    list_local.value.push(item);
  }
}


function incrementQuantity(item) {
  item.quantity++;
  item.price = item.quantity * travelList.value.find((travel) => travel.name === item.name).price;
}

function decrementQuantity(item) {
  if (item.quantity > 0) {
    item.quantity--;
    item.price = item.quantity * travelList.value.find((travel) => travel.name === item.name).price;
  }
}

function removeItem(index) {
  list_local.value.splice(index, 1);
}





const form_costumer = ref({
  name: "",
  phone: "",
  date: "",
  time: ""
});

const showPopup = ref(false);

const totalCost = computed(() => {
    return list_local.value.reduce((acc, item) => acc + item.price, 0);
});

function displayPopup() {
    showPopup.value = true;
}

function togglePopup() {
  showPopup.value = !showPopup.value;
}
// ตัวแปร
const money = ref("");
const travel = ref("");
//const travellist = ref(['ใต้บาดาล','วัด','เขา','ทะเล','ภูเขาไฟ','ค่าเฟ่','ห้าง','บนฟ้า']);
const bookingList = ref([
// "เขา","ทะเล","ภูเขาไฟ","คาเฟ่","บนฟ้า"
]);

// function
function booking(name){
  // name --> +. bookingList[ ]
  bookingList.value.push(name);
}


const travelList = ref([
{name:'เขา', price:500 , img:"https://scontent.fbkk29-5.fna.fbcdn.net/v/t1.15752-9/305297762_1161203148083749_7135020226248945886_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeGrjmSnw5pZ64hIDubVlBN7_xuDjR6-vQz_G4ONHr69DLZ1thgDximQj49PcvCsvCQ8pB4-Mz5YxeJmkyOaQ7Jm&_nc_ohc=EBwp9vqg5f0AX9lM2em&_nc_ht=scontent.fbkk29-5.fna&oh=03_AdRdvRWwTqf3CxFQhPm0UpF6il5mwl-1GyObVKtAzHVu9Q&oe=652B99EC"},
{name:'ทะเล', price:600, img:"https://scontent.fbkk29-8.fna.fbcdn.net/v/t1.15752-9/377107674_627792556205099_2913416014574119500_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeH8tB6n5iKd8JySTazGvHT0nuf9XMFzbpqe5_1cwXNumurN4zlrDMCai9gOqHvJjKPdKh8RTLGGr8Nj79_tXlHI&_nc_ohc=ztVMvkNF-ScAX9_o29x&_nc_ht=scontent.fbkk29-8.fna&oh=03_AdQ9ifhgHekIWTFR3nRHNX5qLV6XR_9u16nNyRkDtCsAqw&oe=652B6E2F"},
{name:'คาเฟ่', price:120, img:"https://scontent.fbkk29-7.fna.fbcdn.net/v/t1.15752-9/251241955_664288884542808_8539650374153743123_n.jpg?_nc_cat=106&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeH5oj5Pdm2VDxJq217SogEXMasL5pnoIWwxqwvmmeghbJ73TsXzAQGV1y7yotJkswooB-MKVDPd9ljQjM7npSYf&_nc_ohc=ApXy1Xg7C6QAX_QMIUy&_nc_ht=scontent.fbkk29-7.fna&oh=03_AdRj9i3JmzEGWgsZ_vMTuk8eoPlDwf-J96uhdamfIPYRsw&oe=652B9C43"},
{name:'ถ้ำ', price:550, img:"https://scontent.fbkk29-9.fna.fbcdn.net/v/t1.15752-9/377109746_1048013709879468_5066377842995027571_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeHD8YoCbM6X8O_Q8NyVrtpDpN0kW7arP7Ok3SRbtqs_sz3quBPji0nhUzHqAQ7eFoswipn9fiEhN4pQl3hrw0Qo&_nc_ohc=KFDX_796hr8AX-TkYYD&_nc_ht=scontent.fbkk29-9.fna&oh=03_AdTgmgCJ6zBQNqhaUxDCHOEOzxNMoNuojmnjSMvOO7bMcA&oe=652B7C38"},
{name:'ร้านอาหาร', price:100, img:"https://scontent.fbkk29-6.fna.fbcdn.net/v/t1.15752-9/377107638_1015105932872458_1666331389039037352_n.webp?stp=dst-webp&_nc_cat=103&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeGknYIs972g9sAqlSLCHbHyzxpZgot3MPzPGlmCi3cw_CzmzCSTdC8UUN4xhXqmUwxmh7TXg4X4M453jZYONtCt&_nc_ohc=i1NeE5H6JVgAX88gnsC&_nc_ht=scontent.fbkk29-6.fna&oh=03_AdSqMZqj7aHECOSUJoc-BQ-82fLF-jPRsEKHOQ49LTcCqg&oe=652B74DD"},
{name:'สวนสนุก', price:220, img:"https://scontent.fbkk29-5.fna.fbcdn.net/v/t1.15752-9/263488888_518255059140193_4325282931557721667_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeF1yXwe8jopdyKKlfvEZwVBtYlr1Zg8qDy1iWvVmDyoPCSFgfQQX_ovW1R7J_nTEIaxff73O1vnxKdVILUS3sCW&_nc_ohc=_1WcHK60lFkAX_fg38A&_nc_ht=scontent.fbkk29-5.fna&oh=03_AdSYNBfwgtjX_rRnlvJAqW-ts73DOPuppA7x5kMqXcd4Uw&oe=652B9335"},
{name:'โรงหนัง', price:180, img:"https://scontent.fbkk29-8.fna.fbcdn.net/v/t1.15752-9/258867377_933527757253810_3670563418848576213_n.jpg?_nc_cat=105&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeEbH4C2LFODH7ClmBlw4K0Lv_YkoSwiIha_9iShLCIiFm6ocO8yOi_wfvFzNBHRG_Bn5QFx8En_YG1IBk-gmOP2&_nc_ohc=Dn1pWiD96qoAX_lkTf4&_nc_ht=scontent.fbkk29-8.fna&oh=03_AdT7gElz4p6OH-JRPWdcEMdWxc3ZAIOa83XHxLl2jHXswQ&oe=652B8DEE"},
{name:'โรงแรม', price:450, img:"https://scontent.fbkk29-6.fna.fbcdn.net/v/t1.15752-9/256307506_1236702526795886_6021207464567372326_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeESbW1WY72q_Z8cRFyjeLFObT6_Mi89k_NtPr8yLz2T87PixCzL6VZVFdQ3R8vRlgWqFEuV1r1T-kVvE893uHLV&_nc_ohc=ttj9fvVS_dUAX8_gWrH&_nc_ht=scontent.fbkk29-6.fna&oh=03_AdTdt0wr5ja-FSIw2djHt0FjsbYLbX5iCozR8wK_LV4QBQ&oe=652B7AE6"},
]);
</script>

<template>
<hahaha v-if="showPopup" />
  <div class="lay" v-if="showPopup">
    <hahaha />
  </div>

  <div class="header">
    <H1>รายการสถานที่ท่องเที่ยว</H1>
  </div>


  <div class="container text-center">
    <div class="row">
      <div class="col" v-for="(i,index) in travelList" :key="index">
        <div class="card" style="width: 18rem;" >
          <img :src="i.img" class="card-img-top">
          <div class="card-body">
            <h3 class="card-title">{{ i.name }}</h3>
            <p>ราคา : {{i.price}}</p>
            <h6></h6>
            <p class="card-text"> 
               <input type="number" class="cout_value " v-model="i.quantity">
            </p>
            <a class="btn btn-primary" @click="list_local_control(i.name, i.quantity)"> จองพื้นที่ & จองโต๊ะ ฯ</a>
          </div>
        </div>
      </div>
    </div>
  </div> 

 

  <h1 style="text-align: center; " v-if="list_local.length>0" class="header">รายการจอง</h1>
  <div class="list_cout text-center">
    <table class="table table-hover" v-if="list_local.length>0">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">ลำดับ</th>
            <th scope="col">ชื่อสถานที่</th>
            <th scope="col">จำนวนที่</th>
            <th scope="col">ราคา</th>
            <th scope="col"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(i,index) in list_local" :key="index" >
            <th scope="row">{{index+1}}</th>
            <td>{{ i.name }}</td>
            <td>
              <div class="quantity-controls">
                <button type="button" class="btn btn-danger"   @click="decrementQuantity(i)" :disabled="i.quantity === 0"> - </button>
                <span>{{ i.quantity }}</span>
                <button type="button" class="btn btn-success" @click="incrementQuantity(i)">+</button>
              </div>
            </td>
            <td>{{ i.price}}</td>
            <td>
              <button type="button" class="btn btn-danger" @click="removeItem(index)" >ยกเลิกรายการ</button>
            </td>
          </tr>
        </tbody>
      </table>  
    </table>
  </div>  

  
  <div class="contrainer_costumer " v-if="list_local.length>0">
  <div class="form_box"> <h2 style="text-align: center;">กรอกข้อมูล</h2></div>
  <form>
    <div class="form_box">
      <label for="name">ชื่อ-นามสกุล </label><br>
      <input type="text" id="name" class="form-control" v-model="form_costumer.name" required>
    </div>
    <div class="form_box">
      <label for="phone">เบอร์โทร </label><br>
      <input type="tel" id="phone" class="form-control" v-model="form_costumer.phone" required>
    </div>
    <div class="form_box">
      <label for="date">วันที่ </label><br>
      <input type="date" id="date" class="form-control" v-model="form_costumer.date" required>
    </div>
    <div class="form_box">
      <label for="time">เวลา </label><br>
      <input type="time" id="time" class="form-control" v-model="form_costumer.time" required>
    </div>
    <div class="form_box">
      <button type="button" class="btn btn-success" @click="togglePopup"> ยืนยันการจอง </button>
    </div>
  </form>
</div>


<div v-if="showPopup" class="overlay">

  <div class="popup">
      <h2 style="text-align: center; color:rgb(225, 255, 0) ;">ยืนยันการจองสำเร็จ</h2>
      <h3 >รายละเอียด</h3>
      <p><strong>ชื่อ-นามสกุล:</strong> {{ form_costumer.name }}</p>
      <p><strong>เบอร์โทร:</strong> {{ form_costumer.phone }}</p>
      <p><strong>วันที่:</strong> {{ form_costumer.date }}</p>
      <p><strong>เวลา:</strong> {{ form_costumer.time }}</p>
      
      <table class="box_table">
          <thead>
              <tr>
                  <th>ลำดับ</th>
                  <th>ชื่อสถานที่</th>
                  <th>จำนวนสถานที่</th>
                  <th>ราคา</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="(i, index) in list_local" :key="index">
                  <td>{{ index + 1 }}</td>
                  <td>{{ i.name }}</td>
                  <td>{{ i.quantity }}</td>
                  <td>{{ i.price }}  บาท </td>
              </tr>
          </tbody>
      </table>

      <p><strong>รวม:</strong> {{ totalCost }} บาท</p>

      <button class="btn btn-danger" @click="showPopup = false">ปิดหน้าต่าง</button>
  </div>
</div>

</template>

<style>
*{
  padding: 5px;

}
.header{
  text-align: center;
  background: #a099ff;
  padding: 25px;
}

.col{
  padding: 10px;
  background: #00385b;
  
}


.contrainer_customer {
  justify-content: center;
  align-items: center;
  margin-left: 20%;
  margin-right: 20%;
}

.form_box{
    justify-content: center;
    align-items: center;
    padding: 5px;
    margin-left: 30%;
    margin-right: 30%;
    background: #dbbced;
}


.lay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0);
  display: flex;
  justify-content: center;
  align-items: center;
}


.popup {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 10px;
  width: 70%;
  max-height: 80%;
  overflow-y: auto;
}



</style>