<script setup lang="ts">
import type { IconComponent } from '@bitrix24/b24ui-nuxt'
import SmileIcon from '@bitrix24/b24icons-vue/outline/SmileIcon'
import HeadsetIcon from '@bitrix24/b24icons-vue/outline/HeadsetIcon'
import ShoppingCartIcon from '@bitrix24/b24icons-vue/outline/ShoppingCartIcon'
import LetterSortDownIcon from '@bitrix24/b24icons-vue/outline/LetterSortDownIcon'
import CalendarIcon from '@bitrix24/b24icons-vue/outline/CalendarIcon'
import MoneyIcon from '@bitrix24/b24icons-vue/outline/MoneyIcon'

interface CardItem {
  id: string
  title: string
  description: string
  icon: IconComponent
  to: string
}

interface CardGroup {
  id: string
  title: string
  items: CardItem[]
}

// Группы карточек
const groups: CardGroup[] = [
  {
    id: 'important',
    title: 'Важные',
    items: [
      {
        id: 'sales-analytics',
        title: 'Анализ продаж',
        description: 'Динамика продаж по месяцам, регионам и категориям',
        icon: MoneyIcon,
        to: '/analytics/sales'
      },
      {
        id: 'financial-reports',
        title: 'Финансовые отчеты',
        description: 'Отчеты о прибыли, убытках и движении денежных средств',
        icon: CalendarIcon,
        to: '/analytics/financial'
      },
      {
        id: 'customer-analytics',
        title: 'Аналитика клиентов',
        description: 'Сегментация клиентов, lifetime value и удержание',
        icon: LetterSortDownIcon,
        to: '/analytics/customers'
      }
    ]
  },
  {
    id: 'secondary',
    title: 'Второстепенные',
    items: [
      {
        id: 'operational-metrics',
        title: 'Операционные метрики',
        description: 'Ключевые показатели эффективности процессов',
        icon: ShoppingCartIcon,
        to: '/analytics/operational'
      },
      {
        id: 'forecast-models',
        title: 'Прогнозные модели',
        description: 'Прогнозирование продаж и трендов на основе исторических данных',
        icon: HeadsetIcon,
        to: '/analytics/forecast'
      },
      {
        id: 'data-export',
        title: 'Экспорт данных',
        description: 'Выгрузка аналитических данных в различных форматах',
        icon: SmileIcon,
        to: '/analytics/export'
      }
    ]
  }
]

const pageTitle = 'Пример 3'
</script>

<template>
  <B24DashboardPanel>
    <template #header>
      <B24DashboardNavbar :title="pageTitle">
        <template #right>
          <B24Button size="sm" label="Обратная связь" />
        </template>
      </B24DashboardNavbar>
    </template>

    <template #body>
      <!-- Группы -->
      <section
        v-for="group in groups"
        :key="group.id"
        class="mb-8 last:mb-0"
      >
        <!-- Заголовок группы -->
        <ProseH2>{{ group.title }}</ProseH2>

        <!-- Карточки -->
        <B24PageGrid>
          <B24PageCard
            v-for="item in group.items"
            :key="item.id"
            v-bind="item"
          />
        </B24PageGrid>
      </section>
    </template>
  </B24DashboardPanel>
</template>

<style scoped>
/* Дополнительные стили при необходимости */
</style>
