<template>
  <div class="sidebar">
    <el-menu
      class="sidebar-el-menu"
      :default-active="onRoutes"
      :collapse="sidebar.collapse"
      text-color="#bfc3dd"
      background-color="#324455"
      active-text-color="#20a0ff"
      unique-opened
      router
    >
      <template v-for="item in items">
        <template v-if="item.subs">
          <el-sub-menu :index="item.index" :key="item.index" v-permission="item.permission">
            <template #title>
              <el-icon>
                <component :is="item.icon"></component>
              </el-icon>
              <span>{{ item.title }}</span>
            </template>
            <template v-for="subItem in item.subs">
              <el-sub-menu
                v-if="subItem.subs"
                :index="subItem.index"
                :key="subItem.index"
                v-permission="item.permission"
              >
                <template #title>{{ subItem.title }}</template>
                <el-menu-item
                  v-for="(threeItem, i) in subItem.subs"
                  :key="i"
                  :index="threeItem.index"
                >
                  {{ threeItem.title }}
                </el-menu-item>
              </el-sub-menu>
              <el-menu-item v-else :index="subItem.index" v-permission="item.permission">
                {{ subItem.title }}
              </el-menu-item>
            </template>
          </el-sub-menu>
        </template>
        <template v-else>
          <el-menu-item :index="item.index" :key="item.index" v-permission="item.permission">
            <el-icon>
              <component :is="item.icon"></component>
            </el-icon>
            <template #title>{{ item.title }}</template>
          </el-menu-item>
        </template>
      </template>
    </el-menu>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useSidebarStore } from '~/store/sidebar'
import { useRoute } from 'vue-router'

const items = [
  {
    icon: 'House',
    index: '/',
    title: '????????????',
    permission: 'dashboard'
  },
  {
    icon: 'Calendar',
    index: '1',
    title: '????????????',
    permission: 'table',
    subs: [
      {
        index: '/table',
        title: '????????????',
        permission: 'table'
      },
      {
        index: '/import',
        title: '??????Excel',
        permission: 'import'
      },
      {
        index: '/export',
        title: '??????Excel',
        permission: 'export'
      }
    ]
  },
  {
    icon: 'DocumentCopy',
    index: '/tabs',
    title: 'tab?????????',
    permission: 'tabs'
  },
  {
    icon: 'Edit',
    index: '3',
    title: '????????????',
    permission: 'form',
    subs: [
      {
        index: '/form',
        title: '????????????',
        permission: 'form'
      },
      {
        index: '/upload',
        title: '????????????',
        permission: 'upload'
      },
      {
        index: '4',
        title: '????????????',
        permission: 'menu',
        subs: [
          {
            index: '/editor',
            title: '??????????????????',
            permission: 'editor'
          },
          {
            index: '/markdown',
            title: 'markdown?????????',
            permission: 'markdown'
          }
        ]
      }
    ]
  },
  {
    icon: 'Help',
    index: '/icon',
    title: '???????????????',
    permission: 'icon'
  },
  {
    icon: 'PieChart',
    index: '/charts',
    title: 'chart??????',
    permission: 'charts'
  },
  {
    icon: 'Warning',
    index: '/permission',
    title: '????????????',
    permission: 'permission'
  },
  {
    icon: 'Switch',
    index: '/axios',
    title: 'axios??????',
    permission: 'axios'
  },
  {
    icon: 'Location',
    index: '/i18n',
    title: '???????????????',
    permission: 'i18n'
  },
  {
    icon: 'CoffeeCup',
    index: '/donate',
    title: '????????????',
    permission: 'donate'
  }
]
const route = useRoute()
const onRoutes = computed(() => {
  return route.path
})

const sidebar = useSidebarStore()
</script>

<style lang="less" scoped>
.sidebar {
  display: block;
  position: absolute;
  left: 0;
  top: 70px;
  bottom: 0;
  overflow-y: scroll;
}
.sidebar::-webkit-scrollbar {
  width: 0;
}
.sidebar-el-menu:not(.el-menu--collapse) {
  width: 250px;
}
.sidebar > ul {
  height: 100%;
}
</style>
