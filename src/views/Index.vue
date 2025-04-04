<!--
 * @Author: ShawnPhang
 * @Date: 2023-09-18 17:34:44
 * @Description: 
 * @LastEditors: Jeremy Yu <https://github.com/JeremyYu-cn>
 * @LastUpdateContent: Typescript desteği
 * @LastEditTime: 2024-02-25 14:51:00
-->
<template>
  <div id="page-design-index" ref="pageDesignIndex" class="page-design-bg-color">
    <div :style="state.style" class="top-nav">
      <div class="top-nav-wrap">
        <div class="top-left">
          <div class="name" @click="jump2home">{{ state.APP_NAME }}</div>
          <div class="operation">
            <div :class="['operation-item', { disable: !undoable }]" @click="undoable ? handleHistory('undo') : ''"><i class="iconfont icon-undo" /></div>
            <div :class="['operation-item', { disable: !redoable }]" @click="redoable ? handleHistory('redo') : ''"><i class="iconfont icon-redo" /></div>
          </div>
          <el-tooltip effect="dark" content="Cetvel" placement="bottom">
            <i style="font-size: 20px" class="icon sd-biaochi extra-operation" @click="changeLineGuides" />
          </el-tooltip>
        </div>
        <HeaderOptions ref="optionsRef" v-model="state.isContinue" @change="optionsChange" />
      </div>
    </div>
    <div class="page-design-index-wrap">
      <widget-panel></widget-panel>
      <design-board class="page-design-wrap" pageDesignCanvasId="page-design-canvas">
        <!-- Tuvalin taşan kısmını gizlemek için, overflow kullanmak hatalı olduğundan -->
        <div class="shelter" :style="{ width: Math.floor((dPage.width * dZoom) / 100) + 'px', height: Math.floor((dPage.height * dZoom) / 100) + 'px' }"></div>
        <!-- Arka plan katmanı sağlar -->
        <div class="shelter-bg transparent-bg" :style="{ width: Math.floor((dPage.width * dZoom) / 100) + 'px', height: Math.floor((dPage.height * dZoom) / 100) + 'px' }"></div>
      </design-board>
      <style-panel></style-panel>
    </div>
    <!-- Cetvel -->
    <line-guides :show="state.showLineGuides" />
    <!-- Yakınlaştırma kontrolü -->
    <zoom-control ref="zoomControlRef" />
    <!-- Sağ tık menüsü -->
    <right-click-menu />
    <!-- Döndürme ve ölçeklendirme bileşeni -->
    <Moveable />
    <!-- Maske yükleme ilerleme çubuğu -->
    <ProgressLoading
      :percent="state.downloadPercent"
      :text="state.downloadText"
      cancelText="İptal"
      @cancel="downloadCancel"
      @done="state.downloadPercent = 0"
    />
  </div>
</template>

<script lang="ts" setup>
import _config from '../config'
import {
  CSSProperties, computed, nextTick,
  onBeforeUnmount, onMounted, reactive, ref,
  getCurrentInstance
} from 'vue'
import { useStore } from 'vuex'
import RightClickMenu from '@/components/business/right-click-menu/RcMenu.vue'
import Moveable from '@/components/business/moveable/Moveable.vue'
import designBoard from '@/components/modules/layout/designBoard/index.vue'
import zoomControl from '@/components/modules/layout/zoomControl/index.vue'
import lineGuides from '@/components/modules/layout/lineGuides.vue'

import shortcuts from '@/mixins/shortcuts'
// import wGroup from '@/components/modules/widgets/wGroup/wGroup.vue'
import HeaderOptions from './components/HeaderOptions.vue'
import ProgressLoading from '@/components/common/ProgressLoading/index.vue'
import { useSetupMapGetters } from '@/common/hooks/mapGetters'
import { useRoute } from 'vue-router'
import { wGroupSetting } from '@/components/modules/widgets/wGroup/groupSetting'

type TState = {
  style: CSSProperties
  downloadPercent: number // İndirme ilerleme yüzdesi
  downloadText: string
  isContinue: boolean
  APP_NAME: string
  showLineGuides: boolean
}

const beforeUnload = function (e: Event): string {
  const confirmationMessage: string = 'Sistem, kaydedilmemiş değişikliklerinizi otomatik olarak kaydetmeyecektir';

  (e || window.event).returnValue = (confirmationMessage as any) // Gecko and Trident
  return confirmationMessage // Gecko and WebKit
}

// mixins: [shortcuts],
!_config.isDev && window.addEventListener('beforeunload', beforeUnload)

const {
  dActiveElement, dHistoryParams, dCopyElement, dPage, dZoom
} = useSetupMapGetters(['dActiveElement', 'dHistoryParams', 'dCopyElement', 'dPage', 'dZoom'])

const state = reactive<TState>({
  style: {
    left: '0px',
  },
  // openDraw: false,
  downloadPercent: 0, // İndirme ilerleme yüzdesi
  downloadText: '',
  isContinue: true,
  APP_NAME: _config.APP_NAME,
  showLineGuides: false,
})
const optionsRef = ref<typeof HeaderOptions | null>(null)
const zoomControlRef = ref<typeof zoomControl | null>(null)
const store = useStore()
const route = useRoute()

// const draw = () => {
//   state.openDraw = true
// }

function jump2home() {
  // const fullPath = window.location.href.split('/')
  // window.open(fullPath[0] + '//' + fullPath[2])
  window.open('https://xp.palxp.cn/')
}

function zoomSub() {
  if (!zoomControlRef.value) return
  zoomControlRef.value.sub()
}

function zoomAdd() {
  if (!zoomControlRef.value) return
  zoomControlRef.value.add()
}

function save() {
  if (!optionsRef.value) return
  optionsRef.value.saveTemplate()
}

defineExpose({
  jump2home,
  zoomSub,
  zoomAdd,
  save,
})

const undoable = computed(() => {
  return !(
    dHistoryParams.value.index === -1 || 
    (dHistoryParams.value === 0 && dHistoryParams.value.length === dHistoryParams.value.maxLength))
})

const redoable = computed(() => {
  return !(dHistoryParams.value.index === dHistoryParams.value.length - 1)
})
// watch: {
//   $route() {
//     console.log('change route', this.$route.query)
//     this.loadData()
//   },
// },

const { handleKeydowm, handleKeyup, dealCtrl } = shortcuts.methods
let checkCtrl: number | undefined

onMounted(() => {
  store.dispatch('initGroupJson', JSON.stringify(wGroupSetting))
  // initGroupJson(JSON.stringify(wGroup.setting))
  window.addEventListener('scroll', fixTopBarScroll)
  // window.addEventListener('click', this.clickListener)
  const instance = getCurrentInstance()
  document.addEventListener('keydown', handleKeydowm(store, checkCtrl, instance, dealCtrl), false)
  document.addEventListener('keyup', handleKeyup(store, checkCtrl), false)
  loadData()
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', fixTopBarScroll)
  const instance = getCurrentInstance()
  // window.removeEventListener('click', this.clickListener)
  document.removeEventListener('keydown', handleKeydowm(store, checkCtrl, instance, dealCtrl), false)
  document.removeEventListener('keyup', handleKeyup(store, checkCtrl), false)
  document.oncontextmenu = null
})
    // ...mapActions(['selectWidget', 'initGroupJson', 'handleHistory']),

function handleHistory(data: string) {
  store.dispatch('handleHistory', data)
}

function changeLineGuides() {
  state.showLineGuides = !state.showLineGuides
}

function downloadCancel() {
  state.downloadPercent = 0
  state.isContinue = false
}

function loadData() {
  // Sayfa yüklemesini başlat
  const { id, tempid, tempType } = route.query
  if (!optionsRef.value) return
  optionsRef.value.load(id, tempid, tempType, async () => {
    if (!zoomControlRef.value) return
    zoomControlRef.value.screenChange()
    await nextTick()
    // Sayfa widget'ını aktif olarak başlat
    store.dispatch('selectWidget', { uuid: '-1' })
    // selectWidget({
    //   uuid: '-1',
    // })
  })
}

function fixTopBarScroll() {
  const scrollTop = document.documentElement.scrollTop || document.body.scrollTop
  state.style.left = -scrollTop + 'px'
}

function clickListener(e: Event) {
  console.log(e)
}

function optionsChange({ downloadPercent, downloadText }: { downloadPercent: number, downloadText: string }) {
  state.downloadPercent = downloadPercent
  state.downloadText = downloadText
}
</script>

<style lang="less" scoped>
@import url('@/assets/styles/design.less');
</style>
