<!--
 * @Author: ShawnPhang
 * @Date: 2022-03-25 15:19:02
 * @Description: Telif Hakkı Bildirimi
 * @LastEditors: ShawnPhang <site: book.palxp.com>
 * @LastEditTime: 2023-08-08 10:09:59
-->
<template>
  <tool-tip title="Sorumluluk Reddi" :width="340" :content="content">
    <div>
      <slot />
    </div>
  </tool-tip>
</template>

<script lang="ts" setup>
import toolTip from '@/components/common/PopoverTip.vue'

const content = 'Bu site kişisel bir projedir. Kullanılan malzemeler ve görseller internetten toplanmıştır. İndirilen çalışmalar yalnızca eğitim, araştırma veya kişisel kullanım amaçlıdır. Ticari kullanım için lisans sağlayamıyoruz.'
</script>

<style lang="less" scoped>
.text {
  color: #33383e;
  font-size: 14px;
}
</style>
