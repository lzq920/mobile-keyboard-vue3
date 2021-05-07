<template>
  <transition name="bounce">
    <div v-if="show" class="keyboard" ref="keyboard" :style="{zIndex:zIndex}">
      <div class="keyboard-tool">
        <div class="keyboard-tool-item" @click="handleCancel">Cancel</div>
        <div class="keyboard-tool-item">{{ keyboardType.name }}</div>
        <div class="keyboard-tool-item" @click="handleConfirm">Confirm</div>
      </div>
      <div class="grid">
        <div class="grid-item" v-for="(item,index) in keyboards" :key="index"
             @click="handleClick(item.action,item.label)">
          {{ item.label }}
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import {ref, computed} from 'vue'

export default {
  name: 'keyboard',
  props: {
    modelValue: String,
    type: {
      type: String,
      default: 'integer'
    },
    zIndex: {
      type: [String, Number],
      default: 1000
    },
    show: {
      type: Boolean,
      default: false
    }
  },
  emits: ["update:modelValue", "cancel", "confirm", "update:show"],
  setup(props, {emit}) {
    const keyboard = ref(null)
    const typeOptions = {
      integer: {
        label: 'Clear',
        action: 'clear',
        name: 'Integer'
      },
      decimal: {
        label: '.',
        action: 'value',
        name: 'Decimal'
      },
      phone: {
        label: 'Clear',
        action: 'clear',
        name: 'Phone'
      },
      card: {
        label: 'X',
        action: 'value',
        name: 'IdCard'
      }
    }
    const keyboardType = computed(() => {
      return typeOptions[props.type]
    });
    const keyboards = computed(() => {
      return [{
        label: "1",
        action: 'value'
      }, {
        label: "2",
        action: 'value'
      }, {
        label: '3',
        action: 'value'
      }, {
        label: "4",
        action: 'value'
      }, {
        label: "5",
        action: 'value'
      }, {
        label: "6",
        action: 'value'
      }, {
        label: "7",
        action: 'value'
      }, {
        label: "8",
        action: 'value'
      }, {
        label: "9",
        action: 'value'
      }, keyboardType.value, {
        label: "0",
        action: 'value'
      }, {
        label: "Delete",
        action: 'delete'
      }]
    })
    const handleClick = (action, label) => {
      switch (action) {
        case 'clear':
          emit('update:modelValue', '')
          break;
        case 'delete':
          emit('update:modelValue', props.modelValue.substr(0, props.modelValue.length - 1))
          break;
        case 'value':
          changeValue(label)
          break;
        default:
          break;
      }
    }
    const changeValue = (val) => {
      let resultStr = props.modelValue + val
      switch (props.type) {
        case 'integer':
          if (!Number.isSafeInteger(parseInt(resultStr))) {
            resultStr = resultStr.substr(0, resultStr.length - 1)
          }
          break;
        case 'decimal':
          let _value = resultStr.split(".");
          if (_value.length === 1) {
            resultStr = _value[0];
          } else if (_value.length === 2) {
            resultStr = _value[0] + '.' + _value[1];
          } else {
            resultStr = _value[0] + '.' + _value[1];
          }
          break;
        case 'phone':
          if (resultStr.length > 11) {
            resultStr = resultStr.substr(0, resultStr.length - 1)
          }
          break;
        case 'card':
          if (resultStr.length > 18) {
            resultStr = resultStr.substr(0, resultStr.length - 1)
          }
          break;
      }
      emit('update:modelValue', resultStr)
    }
    const handleCancel = () => {
      emit("update:show", false)
    }
    const handleConfirm = () => {
      emit("update:show", false)
    }
    return {keyboard, keyboards, handleClick, keyboardType, handleCancel, handleConfirm}
  }
}
</script>

<style scoped>
.bounce-enter-active {
  animation: bounce-in 0.3s;
}

.bounce-leave-active {
  animation: bounce-in 0.3s reverse;
}

@keyframes bounce-in {
  0% {
    transform: translateY(100vw);
  }
  100% {
    transform: translateY(0);
  }
}

.keyboard {
  position: fixed;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100vw;
  height: auto;
  box-shadow: 0px 0px 10px 0px #cccccc;
  padding-bottom: env(safe-area-inset-bottom);
}

.keyboard-tool {
  width: 100vw;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 0px;
  grid-row-gap: 0px;
  box-sizing: border-box;
  background-color: white;
  border-bottom: 1px solid #cccccc;
  border-top: 1px solid #cccccc;
}

.keyboard-tool-item {
  height: 10vw;
  line-height: 10vw;
  text-align: center;
  font-size: 4vw;
  user-select: none;
  cursor: pointer;
}

.grid {
  display: grid;
  width: 100vw;
  height: 80vw;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(4, 1fr);
  grid-column-gap: 0px;
  grid-row-gap: 0px;
  box-sizing: border-box;
  background-color: white;
}

.grid-item {
  height: 20vw;
  font-size: 5vw;
  line-height: 20vw;
  text-align: center;
  transition: all 0.15s;
  user-select: none;
  cursor: pointer;
  border-right: 1px solid #cccccc;
  border-bottom: 1px solid #cccccc;
}

.grid-item:nth-child(3n) {
  border-right: none;
}

</style>
