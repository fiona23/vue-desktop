<template>
  <div class="alert {{type}}" transition="alert">
    <i class="icon d-icon {{iconClass}}"></i>
    <div class="alert-content">
      <span class="alert-title">{{title}}</span>
      <p><slot></slot></p>
      <div class="alert-closebtn" :class="{custom: closeText !== '', 'd-icon': closeText === '', 'd-icon-close': closeText === ''}" v-show="closable" @click="close()">{{closeText}}</div>
    </div>
  </div>
</template>

<style>
  .alert {
    display: inline-block;
    width: 100%;
    padding: 10px 20px;
    box-sizing: border-box;
    border-style: solid;
    border-width: 1px;
    border-radius: 2px;
    position: relative;
    background-color: #fff;
    overflow: hidden;
    transition: opacity .2s;
    opacity: 1;
  }

  .alert.destroyed {
    transition: none;
  }

  .alert.success {
    background-color: #5F9C74;
    border-color: #d6e9c6;
  }

  .alert.error {
    background-color: #e55339;
    border-color: #ebccd1;
  }

  .alert.info {
    background-color: #318cc1;
    border-color: #bce8f1;
  }

  .alert.warning {
    background-color: #E88F31;
    border-color: #faebcc;
  }

  .alert-content {
    float: left;
    display: inline-block;
  }

  .alert .icon {
    display: inline-block;
    box-sizing: border-box;
    height: 42px;
    line-height: 42px;
    text-align: center;
    width: 42px;
    border-radius: 50%;
    font-size: 44px;
    float: left;
    margin-right: 10px;
  }

  .alert .success {
    /*background-color: #f3faf0;*/
    background-color: #5F9C74;
    color: #fff;
  }

  .alert .error {
    background-color: #e55339;
    color: #fff;
  }

  .alert .info {
    background-color: #318cc1;
    color: #fff;
  }

  .alert .warning {
    background-color: #E88F31;
    color: #fff;
  }

  .alert-title {
    font-size: 14px;
    color: #000;
  }

  .alert-content > p {
    color: #fff;
    font-size: 12px;
    margin: 5px 0 0 0;
  }

  .alert-content span {
    color: #fff;
  }

  .alert-closebtn {
    font-size: 20px;
    position: absolute;
    transform: translateY(50%);
    bottom: 50%;
    right: 15px;
    cursor: pointer;
  }

  .alert-closebtn.custom {
    color: #0089dc;
    font-size: 14px;
  }

  .alert-leave {
    opacity: 0;
  }
</style>

<script type="text/ecmascript-6">
  const TYPE_CLASSES_MAP = {
    'success': 'd-icon-success success',
    'warning': 'd-icon-warning warning',
    'error': 'd-icon-error error'
  };

  export default {
    props: {
      title: {
        type: String,
        default: function() {
          return this.$t('alert.title');
        }
      },
      type: {
        type: String,
        default: 'info'
      },
      closable: {
        type: Boolean,
        default: false
      },
      closeText: {
        type: String,
        default: ''
      }
    },

    methods: {
      close() {
        this.$emit('close');
        this.$destroy(true);
      }
    },

    beforeDestroy() {
      this.$el.className += ' destroyed';
    },

    computed: {
      iconClass() {
        return TYPE_CLASSES_MAP[this.type] || 'd-icon-info info';
      }
    }
  }
</script>