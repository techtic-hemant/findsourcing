<template>
  <transition name="modal">
    <div v-show="isOpen" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-cocolntainer">
          <div class="row">
            <div class="col-md-7">
              <div class="color__pickers">
                <b-list-group>
                  <b-list-group-item
                    v-for="item in colors"
                    :key="item"
                    :style="{ background: `#${item}` }"
                  >
                    <b-button @click="() => onSelect(item)">
                      <img src="images/plus-circle.png" alt />
                    </b-button>
                  </b-list-group-item>
                </b-list-group>
              </div>
            </div>
            <div class="col-md-5 select-color">
              <h2>Selected Colors</h2>
              <b-list-group >
                <b-list-group-item v-for="item in selectedColor" :key="item" :style="{ background: `#${item}` }">
                  <a href="#" @click="() => deleteEvent(item)">
                    <img src="images/delete-filled.svg" />
                  </a>
                </b-list-group-item>
              </b-list-group>
              <button
                type="button"
                class="btn btn-default cancel-btn"
                data-dismiss="modal"
                @click="$emit('close')"
              >
                <img src="images/cancel.png" />Cancel
              </button>
              <button type="button" class="btn btn-primary save-btn" @click="saveColor">
                <img src="images/save.png" />save
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>
<script src="https://unpkg.com/vue"></script>
<script>
export default {
  name: "comman-modal",
  props: {
    isOpen: {
      type: Boolean,
    },
    selectedColors: {
      type: Array,
    },
    method: { type: Function },
  },
  data: function () {
    return {
      isOpen: this.isOpen,
      value: "I am the child.",
      selectedColor: this.selectedColors,
      colors: [
        "ffffff",
        "C0C0C0",
        "808080",
        "484848",
        "000000",
        "FF0000",
        "800000",
        "FFDF72",
        "FFFF00",
        "808000",
        "00FF00",
        "008000",
        "0EBA00",
        "00FFFF",
        "008080",
        "0000FF",
        "000080",
        "C371FF",
        "FF00FF",
        "800080",
        "FF9D00",
        "AA6900",
        "00FF89",
        "00AF5E",
        "10643D",
      ],
    };
  },
  methods: {
    onSelect(item) {
       if(!this.selectedColor.includes(item)){
          this.selectedColor.push(item);
       }
    },
    saveColor() {
      this.$emit("save", this.selectedColor);
    },
    deleteEvent(event) {
      this.selectedColor.splice(this.selectedColor.indexOf(event), 1);
    },
  },
  mounted() {
    this.$emit("close");
  },
};
</script>
<style lang="scss">
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}
.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}
.modal-body {
  margin: 20px 0;
}
.modal-default-button {
  float: right;
}
.modal-enter {
  opacity: 0;
}
.modal-leave-active {
  opacity: 0;
}
.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
.modal-cocolntainer {
  max-width: 900px;
  background: #fff;
  border-radius: 10px;
  box-shadow: 0px 0px 15px 0px #585555;
  margin: 0 auto;
  padding: 50px;
  .color__pickers {
    .list-group {
      display: block;
      padding: 0;
      margin: 0;
      max-width: 88.6%;
      border: 1px solid #c7cdd2;
      border-radius: 10px;
      font-size: 0;
      overflow: hidden;
      .list-group-item {
        display: inline-block;
        border: none;
        padding: 0;
        width: 80px;
        height: 80px;
        border-radius: 0;
        button {
          background: none;
          position: absolute;
          border: none;
          padding: 0;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          opacity: 0;
        }
        &:hover {
          button {
            opacity: 1;
          }
        }
      }
    }
  }

  h2 {
    font-size: 20px;
    color: #384b60;
    font-weight: normal;
    margin-bottom: 20px;
  }
  .select-color {
    .list-group {
      overflow: hidden;
      margin-bottom: 50px;
      .list-group-item {
        border: none;
        padding: 0;
        border-radius: 0;
        width: 78px;
        height: 78px;
        a {
          position: absolute;
          right: -200px;
          width: 20px;
          bottom: 20px;
          opacity: 0.6;
        }
      }
    }
    .btn {
      border-radius: 50px;
      color: #35495e;
      border: 1px solid #35495e;
      padding: 7px 25px 9px;
      min-width: 130px;
      img {
        display: inline-block;
        vertical-align: middle;
        margin-right: 10px;
      }
    }
    .save-btn {
      border: 1px solid transparent;
      background: #35495e;
      color: #fff;
      margin-left: 30px;
    }
  }
}
</style>