<template>
  <div class="progress">
    <div class="bar {{barClasses}}" :style="{height: barHeight + 'px'}" v-el:bar>
      <div class="active-bar" :style="{height: barHeight + 'px', width: percent + '%'}"></div>
    </div>
    <span v-if="showPercent" :style="{height: barHeight + 'px', lineHeight: barHeight + 'px'}">{{percent}}%</span>
  </div>
</template>

<style>
  .progress {
    display: table;
    width: 100%;
    padding: 10px;
    box-sizing: border-box;
    position: relative;
    overflow: hidden;
  }

  .progress .bar {
    width: 100%;
    display: table-cell;
    vertical-align: middle;
    background-color: #eee;
    border-radius: 2px;
    overflow: hidden;
  }

  .progress .bar.success .active-bar {
    background-color: #5f9c74;
  }

  .progress .bar.error .active-bar {
    background-color: #e55339;
  }

  .progress .bar.info .active-bar {
    background-color: #318cc1;
  }

  .progress .bar.warning .active-bar {
    background-color: #e88f31;
  }

  .progress span {
    display: table-cell;
    width: 1%;
    min-width: 50px;
    text-align: center;
    vertical-align: middle;
    font-size: 14px;
  }
</style>

<script type="text/ecmascript-6">
  export default {
    props: {
      percent: {
        type: Number,
        default: 0
      },
      type: {
        type: String,
        default: 'info'
      },
      showPercent: {
        type: Boolean,
        default: true
      },
      barHeight: {
        type: Number,
        default: 15
      }
    },

    computed: {
      barClasses() {
        return (this.showPercent ? 'show-info ' : '') + this.type;
      }
    },

    compiled() {
      this.percent = Math.min(this.percent, 100);
    }
  }
</script>