<template>
  <div class="hello">
    <a-layout id="components-layout-demo-top-side-2">
      <a-layout-header class="header">
        <div class="logo" />
        <a-dropdown>
          <a class="ant-dropdown-link" @click="e => e.preventDefault()">
            Hover me <DownOutlined />
          </a>
          <template v-slot:overlay>
            <a-menu>
              <a-menu-item>
                <a href="javascript:;">1st menu item</a>
              </a-menu-item>
              <a-menu-item>
                <a href="javascript:;">2nd menu item</a>
              </a-menu-item>
              <a-menu-item>
                <a href="javascript:;">3rd menu item</a>
              </a-menu-item>
            </a-menu>
          </template>
        </a-dropdown>
      </a-layout-header>
      <a-layout>
        <a-layout-sider width="200" style="background: #fff">
          <a-menu mode="inline">
            <template v-for="(item, index) in data.routerList">
              <template v-if="item.children">
                <a-sub-menu :key="index">
                  <template v-slot:title>
                    <span
                      ><user-outlined /><span>{{ item.title }}</span></span
                    >
                  </template>

                  <a-menu-item
                    v-for="(itemData, index) in item.children"
                    :key="index"
                    ><router-link :to="itemData.path">{{
                      itemData.title
                    }}</router-link></a-menu-item
                  >
                </a-sub-menu>
              </template>
              <template v-else>
                <a-menu-item :key="index">
                  <router-link :to="item.path">
                    <pie-chart-outlined />
                    <span>{{ item.title }}</span>
                  </router-link>
                </a-menu-item>
              </template>
            </template>
          </a-menu>
        </a-layout-sider>
        <a-layout style="padding: 0 24px 24px">
          <a-breadcrumb style="margin: 16px 0">
            <a-breadcrumb-item>Home</a-breadcrumb-item>
            <a-breadcrumb-item>List</a-breadcrumb-item>
            <a-breadcrumb-item>App</a-breadcrumb-item>
          </a-breadcrumb>
          <a-layout-content
            :style="{
              background: '#fff',
              padding: '24px',
              margin: 0,
              minHeight: '280px'
            }"
          >
            {{ data.sum }}
            <router-view />
          </a-layout-content>
        </a-layout>
      </a-layout>
    </a-layout>
  </div>
</template>

<script>
import { UserOutlined, PieChartOutlined } from "@ant-design/icons-vue";
import { reactive, computed } from "vue";
export default {
  name: "HelloWorld",
  components: {
    PieChartOutlined,
    UserOutlined
  },
  setup() {
    const data = reactive({
      sum: computed(() => 1 + 3),
      routerList: [
        {
          path: "/home",
          name: "Home",
          title: "首页"
        },
        {
          path: "/about",
          name: "About",
          title: "列表",
          children: [
            {
              path: "/about",
              name: "About",
              title: "二级页面"
            }
          ]
        }
      ]
    });

    return {
      data
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello,
.ant-layout {
  height: 100%;
}
#components-layout-demo-top-side-2 .logo {
  width: 120px;
  height: 31px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px 28px 16px 0;
  float: left;
}
.ant-dropdown-link {
  float: right;
}
.ant-breadcrumb {
  text-align: left;
}
</style>
