<template>
  <div class="home">
    <b-container>
      <comman-modal :selectedColors="selectedColors" :isOpen="isOpen" @close="closeModal"  @save="handleSave"></comman-modal>
      <div class="product__details">
        <b-row>
          <b-col cols="6">
            <b-row>
              <h1>Cap Toe Sneaker</h1>
            </b-row>
            <b-row class="top__box">
              <b-box v-show="!isSeason" class="add__box--section" @click="isSeason ^= true">
                <i class="fa fa-plus"></i>Add Season
              </b-box>
              <span v-show="isSeason">
                <ul class="add-season">
                  <li v-for="item in season" :key="item">
                    {{item}}
                  </li>
                </ul>
              </span>
              <b-box v-show="!isLabel" class="add__box--label" @click="isLabel ^= true">
                <i class="fa fa-plus"></i>Add Label
              </b-box>
              <span v-show="isLabel">
                <ul class="add-label">
                  <li v-for="item in label" :key="item">
                    {{item}}
                  </li>
                </ul>
              </span>
            </b-row>
          </b-col>
          <b-col cols="6">
            <div class="right__badge">
              <b-badge class="badge__right--first" variant="primary">Idea</b-badge>
              <b-badge class="badge__right--second" variant="warning">In Development</b-badge>
            </div>
          </b-col>
        </b-row>
        <b-row class="color__option">
          <b-col cols="5">
            <div class="color__left">
              <span>colors</span>
              <a v-if="!selectedColors.length"  @click="isOpen = !isOpen;" class="option__button">
                <img src="images/add.png" alt />
                <em>Add</em>
              </a>
              <div v-if="!isOpen && selectedColors.length > 0"  @click="isOpen = !isOpen;" class="add__color">
                <ul>
                  <li v-for="item in selectedColors" :key="item" :style="{ background: `#${item}` }">{{ item }}</li>
                </ul>
              </div>
              <div class="color__btm__option">
                <div class="btm__option__left">
                    <b-img src="images/supplier-large.svg"></b-img>
                    <span v-show="!isSupplier">
                    <a @click="isSupplier ^= true" class="option__button">
                      <img src="images/plus-circle.png" alt />
                      <em>Add Supplier</em>
                    </a>
                  </span>
                  <span v-show="isSupplier">
                    <ul class="add__supplier_open">
                        <li><img src="images/abw.svg" /><em>Albano Perreira</em></li>
                        <li><img src="images/abw.svg" /><em>Shoelutions</em></li>
                      </ul>
                  </span>
                </div>
                <div class="btm__option__left">
                  <span v-show="!isPrice">
                    <b-img src="images/retail-price-large.svg"></b-img>
                    <a @click="isPrice ^= true" class="option__button">
                      <img src="images/plus-circle.png" alt />
                      <em>Add Pricing</em>
                    </a>
                  </span>
                  <div class="price-data" v-show="isPrice">
                   <ul>
                     <li>
                      <figure><img src="images/price1.png" /></figure>
                      <font>&euro; 30</font>
                      <span>Factory price</span>
                      <em>&#10005;</em>
                    </li>
                    <li>
                      <figure><img src="images/price2.png" /></figure>
                      <font>5.5</font>
                      <span>markup</span>
                      <em>&#x0003D;</em>
                    </li>
                    <li>
                      <figure><img src="images/retail-price-large.svg" /></figure>
                      <font>&euro; 185</font>
                      <span>retail price</span>
                    </li>
                   </ul>
                 </div>
                </div>
              </div>
            </div>
          </b-col>
          <b-col cols="7">
            <div class="shoes__upper">
              <b-img src="images/shoes.svg"></b-img>
              <a class="option__button">
                <img src="images/blank-img.png" alt />
                <em>Add Pricing</em>
              </a>
            </div>
          </b-col>
        </b-row>
      </div>
    </b-container>
  </div>
</template>
<script>
import commanModal from "./comman-modal.vue";
export default {
  name: "Home",
  components: {
    commanModal,
  },
  props: ["product"],
  data: function () {
    return {
      isSeason: false,
      isLabel: false,
      isSupplier: false,
      isPrice: false,
      isOpen: false,
      season: ["AW21", "SS21", "SS22","3+"],
      label: ["Core", "Waterprrof", "Vegan", "+2"],
      // supplier: ["Albano Perreira", "Shoelutions"],
      selectedColors : []
    };
  },
  methods: {
    closeModal() {
      this.isOpen = false;
    },
    handleSave(value) {
      //console.log(value, 'value');
      if(value.length){
        value.map((item)=>{
          if(!this.selectedColors.includes(item)){
            this.selectedColors.push(item);
          }          
        })
      }
      
      //console.log(this.selectedColors, 'this.selectedColors');
      this.isOpen = false;
    },
  },
};
</script>
<style lang="scss">
.product__details {
  max-width: 95%;
  margin: 0 auto;
  h1 {
    font-size: 20px;
    margin-bottom: 13px;
  }
  .top__box {
    .add {
      &__box {
        &--section {
          background: #fff;
          color: #44576A;
          border-radius: 4px;
          display: block;
          font-size: 12px;
          padding: 3px 19px;
          margin-right: 10px;
          &:last-child {
            margin-right: 0;
          }
          i {
            font-size: 8px;
            margin-right: 6px;
          }
        }
        &--label {
          background: #B1B1B1;
          color: #fff;
          border-radius: 4px;
          display: block;
          font-size: 12px;
          padding: 3px 19px;
          i {
            font-size: 8px;
            margin-right: 6px;
          }
        }
      }
    }
  }
  .right__badge {
    text-align: right;
    .badge {
      font-size: 12px;
      border-radius: 30px;
      min-width: 116px;
      line-height: 22px;
      height: 25px;
      color: #fff;
      text-align: center;
      padding: 0;
      margin-right: 10px;
      &:last-child {
        margin-right: 0;
      }
      &__right {
        &--first {
          background: #3498DB;
        }
        &--second {
          background: #F7BA64;
        }
      }
    }
  }
  .color__option {
    margin-top: 45px;
    img {
      display: inline-block;
      vertical-align: middle;
      max-width: 20px;
      margin-right: 10px;
    }
    em {
      display: inline-block;
      vertical-align: middle;
      font-style: normal;
      font-size: 14px;
    }
    text-align: left;
    .col-4 {
      padding-left: 0;
    }
    span {
      display: block;
      color: #929CA7;
      text-transform: uppercase;
      font-size: 16px;
      margin-bottom: 10px;
    }
    .option__button {
      background: #fff;
      color: #35495E;
      border: 1px dashed #929CA7;
      padding: 15px 44px;
      border-radius: 5px;
      display: inline-block;
      min-width: 177px;
      font-size: 16px;
      cursor: pointer;
      &:hover {
        text-decoration: none;
      }
    }
    .color__btm__option {
      margin-top: 50px;
      .btm__option__left {
        width: 50%;
        display: inline-block;
        vertical-align: middle;
        img {
          opacity: 0.5;
          max-width: 30px;
          margin-right: 20px;
        }
        a {
          display: inline-block;
          vertical-align: middle;
          padding: 23px 33px;
          min-width: initial;
          margin-left: 10px;
        }
        .option__button {
          img {
            opacity: 1;
            margin-right: 10px;
          }
        }
        span{
          display: inline-block;
          vertical-align: middle;
          margin-bottom: 0;
        }
        .add__supplier_open{
          padding: 0;
          min-width: 160px;
          margin: 0;
          li{
            list-style: none;
            color: #35495E;
            margin-bottom: 4px;
            &:last-child{
              margin-bottom: 0;
            }
            img{
              display: inline-block;
              vertical-align: middle;
              opacity: 1;
              margin-right: 10px;
              max-width: 20px;
            }
            em{
              display: inline-block;
              vertical-align: middle;
            }
          }
        }
        .price-data{
          display: inline-block;
          vertical-align: middle;
          max-width: 80%;
          ul{
            display: flex;
            margin-top: 10px;
            padding: 0;
            li{
              list-style: none;
              display: inline-block;
              vertical-align: middle;
              text-align: center;
              position: relative;
              figure{
                img{
                  opacity: 1;
                  margin: 0 auto;
                  margin-bottom: 8px;
                }
              }
              font{
                color: #35495E;
                font-weight: 600;
                font-size: 20px;
              }
              span{
                font-size: 12px;
              }
              em{
                position: absolute;
                top: 50%;
                transform: translateY(-50%);
                right: 0;
              }
            }
          }
        }
      }
    }
    .shoes__upper {
      &:after {
        content: "";
        display: block;
        clear: both;
      }
      position: relative;
      img {
        max-width: 88%;
        opacity: 0.3;
        float: right;
      }
      .option__button {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        img {
          opacity: 0.5;
          float: none;
          max-width: 100%;
        }
      }
    }
  }
  .add-season{
     display: flex;
     padding: 0;
     margin-bottom: 0;
     li{
       list-style: none;
       background: #fff;
      color: #44576A;
      border-radius: 4px;
      display: block;
      font-size: 12px;
      padding: 3px 19px;
      margin-right: 10px;
      &:nth-child(1){
        border: 1px solid #8C9DCC;
      }
      &:nth-child(2){
        border: 1px solid #E2C35B;
      }
      &:nth-child(3){
        border: 1px solid #8C9DCC;
      }
     }
  }
  .add-label{
    display: flex;
    padding: 0;
    margin-bottom: 0;
    margin-left: 50px;
    li{
      background: #B1B1B1;
      color: #fff;
      border-radius: 4px;
      display: block;
      font-size: 12px;
      padding: 3px 19px;
      margin-right: 10px;
      &:last-child{
        margin-right: 0;
      }
      &:nth-child(1){
        background: #84C66C;
      }
      &:nth-child(2){
        background: #4A75A7;
      }
      &:nth-child(3){
        background: #669B45;
      }
    }
  }
  .add__color{
    ul{
      padding: 0;
      margin: 0;
      max-width: 300px;
      margin-top: 30px;
      li{
        display: inline-block;
        border-radius: 30px;
        background: #333333;
        color: #fff;
        font-size: 12px;
        padding: 2px 19px;
        min-width: 90px;
        text-align: center;
        border: 1px solid transparent;
        margin-right: 10px;
        margin-bottom: 10px;
        &:nth-child(2){
          background: #fff;
          border: 1px solid #35495e;
          color: #35495e;
        }
        &:nth-child(3){
          background: #967252;
        }
        &:nth-child(4){
          background: #de5656;
        }
        &:nth-child(5){
          background: #569ade;
        }
        &:nth-child(6){
          background: #459048;
        }
      }
    }
  }
}
</style>