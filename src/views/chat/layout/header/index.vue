<script lang="ts" setup>
import { computed } from 'vue'
import { SvgIcon } from '@/components/common'
import { useAppStore, useChatStore } from '@/store'

const appStore = useAppStore()
const chatStore = useChatStore()

const collapsed = computed(() => appStore.siderCollapsed)

function handleAdd() {
  chatStore.addHistory({ title: 'New Chat', uuid: Date.now(), isEdit: false })
}

function handleUpdateCollapsed() {
  appStore.setSiderCollapsed(!collapsed.value)
}

function handleDoubleClick() {
  const scrollRef = document.querySelector('#scrollRef')
  if (scrollRef)
    scrollRef.scrollTop = 0
}
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-30 border-b dark:border-neutral-800 bg-white/80 dark:bg-black/20 backdrop-blur"
    @dblclick="handleDoubleClick"
  >
    <div class="relative flex items-center justify-between h-14">
      <button class="flex items-center justify-center w-11 h-11" @click="handleUpdateCollapsed">
        <SvgIcon v-if="collapsed" class="text-2xl" icon="ri:align-justify" />
        <SvgIcon v-else class="text-2xl" icon="ri:align-right" />
      </button>
      <button class="flex items-center justify-center w-11 h-11" @click="handleAdd">
        <SvgIcon class="text-2xl" icon="ri:add-fill" />
      </button>
    </div>
  </header>
</template>
