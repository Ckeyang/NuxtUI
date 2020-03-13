<script>
import defaultClass from "../plugins/themes/default/NDialog";
const TAGDIV = "div";
const TAGSPAN = "span";
const TAGI = "i";
const emptyString = "";
const emitUpdateVisible = "update:visible";
export default {
  name: "NDialog",
  props: {
    visible: {
      type: Boolean,
      default: () => {
        return false;
      }
    }, //是否可见
    title: { type: String, default: "" }, //标题
    width: { type: String, default: "240px" }, //宽度
    height: { type: String, default: "240px" }, //高度
    fullscreen: {
      type: Boolean,
      default: () => {
        return false;
      }
    }, //是否全屏
    modal: {
      type: Boolean,
      default: () => {
        return true;
      }
    }, //是否要modal
    showClose: {
      type: Boolean,
      default: () => {
        return true;
      }
    }, //是否要关闭按钮
    closeOnClickModal: {
      type: Boolean,
      default: () => {
        return true;
      }
    } //是否点击modal 关闭 dialog
  },
  computed: {
    /**
     * 获取modalClass
     */
    getModalClass() {
      let classNames = [];
      classNames.push(defaultClass.modalWidth);
      classNames.push(defaultClass.modalHeight);
      classNames.push(defaultClass.modalBackgroundColor);
      classNames.push(defaultClass.modalPosition);
      classNames.push(defaultClass.modalFlexCenter);
      return classNames;
    },
    /**
     * 获取dialogClass
     */
    getDialogClass() {
      let classNames = [];
      classNames.push(defaultClass.dialogBorderRadius);
      classNames.push(defaultClass.dialogBackgroundColor);
      classNames.push(defaultClass.dialogCenter);
      return classNames;
    }
  },
  methods: {
    /**
     * 点击modal 关闭 dialog
     */
    closeDialogOnModal() {
      this.closeOnClickModal ? this.$emit(emitUpdateVisible, false) : null;
    },
    /**
     * 关闭 dialog
     */
    closeDialog() {
      this.$emit(emitUpdateVisible, false);
    },
    /**
     * 创建modal
     */
    createModal(h) {
      return h(
        TAGDIV,
        {
          class: this.getModalClass,
          on: {
            click: this.closeDialogOnModal
          }
        },
        [this.createDialog(h)]
      );
    },
    /**
     * 创建dialog
     */
    createDialog(h) {
      return h(
        TAGDIV,
        {
          class: this.getDialogClass,
          style: {
            width: this.width,
            minHeight: this.height
          },
          on: {
            click: event => {
              event.stopPropagation();
            }
          }
        },
        [this.createTitle(h), this.createContainer(h)]
      );
    },
    /**
     * 创建标题栏
     */
    createTitle(h) {
      return h(
        TAGDIV,
        {
          class: [defaultClass.titleClass]
        },
        [
          this.$slots.title
            ? this.$slots.title
            : h(TAGSPAN, { class: [defaultClass.textSize] }, this.title),
          this.showClose
            ? h(
                TAGSPAN,
                {
                  class: [defaultClass.pointer],
                  on: { click: this.closeDialog }
                },
                [h(TAGI, { class: [defaultClass.pointClass] })]
              )
            : emptyString
        ]
      );
    },
    /**
     * 创建内容栏
     */
    createContainer(h) {
      return h(
        TAGDIV,
        {
          class: [defaultClass.containerClass],
          style: {
            height: this.height,
            overflow: defaultClass.containerOverflow
          }
        },
        this.$slots.default
      );
    }
  },
  /**
   * 渲染
   */
  render: function(h) {
    if (this.visible) {
      return this.modal ? this.createModal(h) : h(TAGDIV, this.createDialog(h));
    }
  }
};
</script>
<style>
.bg-gray-500-opacity75 {
  background-color: #000000c2;
}
</style>
