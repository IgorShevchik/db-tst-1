<script setup lang="ts">
import type { IconComponent } from '@bitrix24/b24ui-nuxt'
import GraphsDiagramIcon from '@bitrix24/b24icons-vue/outline/GraphsDiagramIcon'
import StatisticsArrowIcon from '@bitrix24/b24icons-vue/outline/StatisticsArrowIcon'
import SpeedMeterIcon from '@bitrix24/b24icons-vue/outline/SpeedMeterIcon'

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
    id: 'monthly',
    title: 'Ежемесячные',
    items: [
      {
        id: 'sales-report',
        title: 'Отчет по продажам',
        description: 'Детальный анализ продаж за месяц, динамика и тренды',
        icon: GraphsDiagramIcon,
        to: '/demo/reports/sales'
      },
      {
        id: 'traffic-analysis',
        title: 'Анализ трафика',
        description: 'Источники трафика, конверсия и поведение пользователей',
        icon: StatisticsArrowIcon,
        to: '/demo/reports/traffic'
      },
      {
        id: 'financial-report',
        title: 'Финансовый отчет',
        description: 'Доходы, расходы, прибыль и финансовые показатели',
        icon: SpeedMeterIcon,
        to: '/demo/reports/finance'
      }
    ]
  }
]

const pageTitle = 'Перечень отчетов'
</script>

<template>
  <B24DashboardPanel>
    <template #header>
      <B24DashboardNavbar :title="pageTitle">
        <template #right>
          <B24Button size="sm" label="Фильтр" />
          <B24Button size="sm" variant="primary" label="Создать отчет" />
        </template>
      </B24DashboardNavbar>
    </template>

    <template #body>
      <!-- Группы -->
      <section
        v-for="group in groups"
        :key="group.id"
        class="mb-8"
      >
        <!-- Заголовок группы -->
        <ProseH2>{{ group.title }}</ProseH2>

        <!-- Карточки -->
        <B24PageGrid class="lg:grid-cols-3">
          <B24PageCard
            v-for="item in group.items"
            :key="item.id"
            :title="item.title"
            :description="item.description"
            :icon="item.icon"
            :to="item.to"
            :b24ui="{
              container: 'overflow-hidden gap-y-1.5 p-4 sm:p-4',
              wrapper: 'items-center flex-row gap-4',
              leading: 'p-2.5 rounded-full bg-primary/10 ring ring-inset ring-primary/25 mb-0',
              title: 'text-description font-bold text-md'
            }"
          />
        </B24PageGrid>
      </section>
    </template>
  </B24DashboardPanel>
</template>