<template>
  <div class="containerFluid">
    <div class="container">
      <div class="menuNav">

        <div class="menuNav__firstItem menuNav__content">
          <span>
            <i class="fa fa-th-list" aria-hidden="true"></i>&nbsp;商品分类
          </span>
        </div>

        <div class="menuNav__secondItem menuNav__content">
          <el-link :underline="false">
            <i class="fa fa-cart-plus" aria-hidden="true"></i>&nbsp;天猫超市
          </el-link>
        </div>

        <div class="menuNav__secondItem menuNav__content">
          <el-link :underline="false">
            <i class="fa fa-globe" aria-hidden="true"></i>&nbsp;天猫国际
          </el-link>
        </div>

        <div
          class="menuNav__normalItem menuNav__content"
          v-for="item in menuNavItem"
          :key="item.id">
          <el-link :underline="false" v-text="item.name" @click="test(item.id)"></el-link>
        </div>

      </div>
    </div>
  </div>
</template>
<script>
import { pageResProcess } from '../assets/util/ResProcess';

export default {
  name: 'menuNav',
  components: {},
  created() {
    this.$store.dispatch('home/getMenuNavItem')
      .then((data) => {
        pageResProcess(data);
      });
  },
  mounted() {},
  data() {
    return {};
  },
  computed: {
    menuNavItem() {
      return this.$store.state.home.menuNavItem;
    },
  },
  watch: {},
  methods: {
    test(val) { // todo
      console.log(val);
    },
  },
};
</script>
<style scoped lang="scss">
  // 导入Scss
  @import "../assets/scss/constant";
  @import "../assets/scss/mixins";
  // 变量定义
  $menu--background-color: #DD2727;
  // Scss样式
  .containerFluid {
    @include containerFluid;
    background-color: $menu--background-color;
    height: 38px;
  }

  .container {
    @include container;
  }

  .menuNav {
    line-height: 35px;
    font-size: 16px;

    a, span {
      color: $color-white;
    }

    &__content {
      display: inline-block;

      &:hover {
        background-color: $color-primary;
      }

      a {
        margin: 0 10px 0 10px;

        &:hover {
          color: $color-white;
        }
      }
    }

    &__content + .menuNav__content {
      margin-left: 20px;
    }

    &__firstItem {
      width: 180px;
      height: 37px;
      background-color: $color-primary;
      padding-left: 20px;

      span {
        font-size: 17px;
        font-weight: 700;
      }
    }
  }
</style>
