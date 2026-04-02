<script setup lang="ts">
import MessagesIcon from '@bitrix24/b24icons-vue/outline/MessagesIcon'
import GroupIcon from '@bitrix24/b24icons-vue/outline/GroupIcon'
import SettingsIcon from '@bitrix24/b24icons-vue/outline/SettingsIcon'

const cards = ref([
  {
    title: 'Inbox',
    description: 'Входящие сообщения',
    icon: MessagesIcon,
    to: '/inbox'
  },
  {
    title: 'Customers',
    description: 'Список клиентов',
    icon: GroupIcon,
    to: '/customers'
  },
  {
    title: 'Settingss',
    description: 'Настройки приложения',
    icon: SettingsIcon,
    to: '/settings'
  }
])
</script>

<template>
  <B24DashboardPanel id="{pagePanelId}">
    <template #header>
      <B24DashboardNavbar title="{pageTitle}">
        <template #right>
          <B24Button size="sm" label="Feedback" />
        </template>
      </B24DashboardNavbar>
    </template>
    <template #body>
      <section>
        <ProseH2>{firstGroupTitle}</ProseH2>
        <B24PageGrid>
          <B24PageCard
            v-for="(card, index) in cards"
            :key="index"
            v-bind="card"
          />
        </B24PageGrid>
      </section>

      <section>
        <ProseH2>{SecondGroupTitle}</ProseH2>
        <B24PageGrid>
          <B24PageCard
            v-for="(card, index) in cards"
            :key="index"
            v-bind="card"
          />
        </B24PageGrid>
      </section>
    </template>
  </B24DashboardPanel>
</template>
