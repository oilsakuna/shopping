<template>
  <div id="app">
    <div class="container">
      <img
        src="https://d2pa5gi5n2e1an.cloudfront.net/webp/th/images/article/2917_TH/summary_snp.jpg"
        class="img-circle"
        alt="Cinque Terre"
        width="1110"
        height="400"
      />
      <div class="head">OilCosmetics.Com</div>

      <hr />
      <div class="row">
        <div class="col-md-2" v-for="it in products" :key="it.it">
          <div class="card h-100">
            <img :src="it.image" class="car-img-top" />
            <div class="card-body">
              <h4 class="card-title">{{ it.n }}</h4>
              <p class="card-text">ราคา {{ it.price }} บาท</p>
            </div>
            <div class="card-footer">
              <button class="btn btn-warning" @click="addCart(it)">
                หยิบลงรถเข็น
              </button>
              <div></div>
            </div>
          </div>
        </div>
        <div class="col-md-6" v-if="carts != 0">
          <h2>
            -->รถเข็น
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="30"
              height="30"
              fill="currentColor"
              class="bi bi-cart4"
              viewBox="0 0 16 16"
            >
              <path
                d="M0 2.5A.5.5 0 0 1 .5 2H2a.5.5 0 0 1 .485.379L2.89 4H14.5a.5.5 0 0 1 .485.621l-1.5 6A.5.5 0 0 1 13 11H4a.5.5 0 0 1-.485-.379L1.61 3H.5a.5.5 0 0 1-.5-.5zM3.14 5l.5 2H5V5H3.14zM6 5v2h2V5H6zm3 0v2h2V5H9zm3 0v2h1.36l.5-2H12zm1.11 3H12v2h.61l.5-2zM11 8H9v2h2V8zM8 8H6v2h2V8zM5 8H3.89l.5 2H5V8zm0 5a1 1 0 1 0 0 2 1 1 0 0 0 0-2zm-2 1a2 2 0 1 1 4 0 2 2 0 0 1-4 0zm9-1a1 1 0 1 0 0 2 1 1 0 0 0 0-2zm-2 1a2 2 0 1 1 4 0 2 2 0 0 1-4 0z"
              />
            </svg>
          </h2>
          <hr />
          <table class="table">
            <thead class="table-danger">
              <tr>
                <th scope="col">ชื่อ</th>
                <th scope="col">ราคา</th>
                <th scope="col">จำนวน</th>
                <th scope="col">รวม</th>
                <th scope="col">ลบ</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="product in carts" :key="product.product">
              
                <td>{{ product.n }}</td>
                <td>{{ product.price }}</td>
                <td class="container">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="16"
                    height="16"
                    fill="currentColor"
                    class="bi bi-align-end qty-minus"
                    viewBox="0 0 16 16"
                    @click="minusQty(product)"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M14.5 1a.5.5 0 0 0-.5.5v13a.5.5 0 0 0 1 0v-13a.5.5 0 0 0-.5-.5z"
                    />
                    <path
                      d="M13 7a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v2a1 1 0 0 0 1 1h10a1 1 0 0 0 1-1V7z"
                    />
                  </svg>
                  {{ product.qty }}
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="16"
                    height="16"
                    fill="currentColor"
                    class="bi bi-align-center qty-plus"
                    viewBox="0 0 16 16"
                    @click="plusQty(product)"
                  >
                    <path
                      d="M8 1a.5.5 0 0 1 .5.5V6h-1V1.5A.5.5 0 0 1 8 1zm0 14a.5.5 0 0 1-.5-.5V10h1v4.5a.5.5 0 0 1-.5.5zM2 7a1 1 0 0 1 1-1h10a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V7z"
                    />
                  </svg>
                </td>
                <td>{{ product.total }}</td>
                <td>
                  <button @click="removeProduct(product)" class="btn-danger">
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="16"
                      height="16"
                      fill="currentColor"
                      class="bi bi-trash-fill"
                      viewBox="0 0 16 16"
                    >
                      <path
                        d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"
                      />
                    </svg>
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
          <h4 align="Right">ยอดชำระเงิน {{ total() }} บาท</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      carts: [],
      EYESHADOW: 0,
      Mascara: 0,
      FOUNDATION: 0,
      POWDER: 0,
      LIP: 0,
      Cement: 0,
      Concealer: 0,
      CREAM: 0,
      EYESHADOWS: 0,
      PowderFoundation: 0,
      Primer: 0,
      Lipstick: 0,
      products: [
        {
          id: 1,
          n: "SHIMMER WASH EYE SHADOW",
          price: 1300,
          image:
            "https://www.bobbibrown.co.th/media/export/cms/products/415x415/bb_prod_E4PA_415x415_0.jpg",
          active: false,
        },
        {
          id: 2,
          n: "EYE OPENING MASCARA",
          price: 690,
          image:
            "https://www.bobbibrown.co.th/media/export/cms/products/415x415/bb_prod_EETT_415x415_0.jpg",
          active: false,
        },
        {
          id: 3,
          n: "SKIN FOUNDATION SPF 15",
          price: 2199,
          image:
            "https://www.bobbibrown.co.th/media/export/cms/products/415x415/bb_prod_E2LE_415x415_0.jpg",
          active: false,
        },
        {
          id: 4,
          n: "BRONZING POWDER",
          price: 999,
          image:
            "https://www.bobbibrown.co.th/media/export/cms/products/415x415/bb_prod_E1FX_415x415_0.jpg",
          active: false,
        },
        {
          id: 5,
          n: "RICH LIP COLOR",
          price: 890,
          image:
            "https://www.bobbibrown.co.th/media/export/cms/products/415x415/bb_prod_E8Y8_415x415_0.jpg",
          active: false,
        },
        {
          id: 6,
          n: "MEDIUM BROW KIT",
          price: 1199,
          image:
            "https://www.bobbibrown.co.th/media/export/cms/products/415x415/bb_prod_E80N_415x415_0.jpg",
          active: false,
        },
        {
          id: 7,
          n: "Instant Full Cover Concealer",
          price: 899,
          image:
            "https://backend.central.co.th/media/catalog/product/C/D/CDS14170409.jpg?impolicy=resize&width=553",
          active: false,
        },
        {
          id: 8,
          n: "VITAMIN ENRICH CREAM",
          price: 1599,
          image:
            "https://backend.central.co.th/media/catalog/product/C/D/CDS86731300.jpg?impolicy=resize&width=553",
          active: false,
        },
        {
          id: 9,
          n: "อายแชโดว์ The Essential",
          price: 1299,
          image:
            "https://backend.central.co.th/media/catalog/product/c/d/cds31318785-1.jpg?impolicy=resize&width=440",
          active: false,
        },
        {
          id: 10,
          n: "Skin Weightless Powder Foundation (รีฟิล)",
          price: 1590,
          image:
            "https://www.bobbibrown.co.th/media/export/cms/products/v2_1080x1080/bb_sku_EATE05_1080x1080_0.jpg",
          active: false,
        },
        {
          id: 11,
          n: "ไพรเมอร์ Primer Plus Protection SPF 50",
          price: 1890,
          image:
            "https://encrypted-tbn1.gstatic.com/shopping?q=tbn:ANd9GcSJW2EGJQBHjOa1pAUwU4q8RDww_yzjkMNF-ZWCzk_HV_rDob4uISIUqAEOWyP3LI3ORIklVXw&usqp=CAE",
          active: false,
        },
        {
          id: 12,
          n: "ลิปสติก Luxe Defining Lipstick Limited Edition",
          price: 799,
          image:
            "https://backend.central.co.th/media/catalog/product/c/d/cds70208610-1.jpg?impolicy=resize&width=553",
          active: false,
        },
      ],
    };
  },
  methods: {
    addCart: function (it) {
      if (it.id == 1) {
        //ซื้อEYESHADOW
        this.EYESHADOW += 1;
        if (this.EYESHADOW <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 2) {
        //ซื้อMascara
        this.Mascara += 1;
        if (this.Mascara <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 3) {
        //ซื้อรองพื้น
        this.FOUNDATION += 1;
        if (this.FOUNDATION <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 4) {
        //ซื้อแป้ง
        this.POWDER += 1;
        if (this.POWDER <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 5) {
        //ซื้อลิป
        this.LIP += 1;
        if (this.LIP <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 6) {
        //ซื้อCement
        this.Cement += 1;
        if (this.Cement <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 7) {
        //ซื้อConcealer
        this.Concealer += 1;
        if (this.Concealer <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 8) {
        //ซื้อครีม
        this.CREAM += 1;
        if (this.CREAM <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 9) {
        //ซื้อEYESHADOWS
        this.EYESHADOWS += 1;
        if (this.EYESHADOWS <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 10) {
        //ซื้อPowderFoundation
        this.PowderFoundation += 1;
        if (this.PowderFoundation <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 11) {
        //ซื้อPrimer
        this.Primer += 1;
        if (this.Primer <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (it.id == 12) {
        //ซื้อLipstick
        this.Lipstick += 1;
        if (this.Lipstick <= 1) {
          //ซื้อรอบเดียว
          this.pushData(it);
        } else {
          //รายการเดียวกัน
          var found = this.findIndex(it);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      }
    },
    pushData(it) {
      this.carts.push({
        id: it.id,
        n: it.n,
        price: it.price,
        image: it.image,
        qty: 1,
        total: it.price,
      });
    },
    findIndex: function (it) {
      for (var i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id == it.id) {
          return i; //ตำแหนงสินค้าที่ค้นเจอ
        }
      }
      return -1;
    },
    minusQty: function (product) {
      product.qty -= 1;
      if (product.qty <= 1) {
        product.qty = 1;
      }
      product.total = product.price * product.qty;
    },
    plusQty: function (product) {
      product.qty += 1;
      product.total = product.price * product.qty;
    },
    removeProduct(product) {
      if (confirm("คุณต้องการลบหรือไม่ ? ")) {
        var index = this.carts.indexOf(product);
        this.carts.splice(index, 1);
        if (product.id == 1) {
          this.coffee = 0;
        } else {
          this.tea = 0;
        }
      }
    },
    total: function () {
      var sum = 0;
      this.carts.forEach(function (it) {
        sum += it.total;
      });
      return sum;
    },
  },
};
</script>
<style scoped>
.qty-minus {
  cursor: pointer;
  margin-right: 20px;
}
.qty-plus {
  cursor: pointer;
  margin-left: 20px;
}

.head {
  background-color: rgb(230, 31, 147);
  color: rgb(250, 252, 249);
  height: 44px;
  display: flex;
  align-items: center;
  font-size: 28px;
  font-weight: 800;
}
</style>>


