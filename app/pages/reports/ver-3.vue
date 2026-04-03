<script setup lang="ts">
import { onMounted } from 'vue'
import { useB24 } from '~/composables/useB24'

// Импорт иконок для группы Продажи
import GraphsDiagramIcon from '@bitrix24/b24icons-vue/main/GraphsDiagramIcon'
import Funnel1Icon from '@bitrix24/b24icons-vue/crm/Funnel1Icon'
import Conversion1Icon from '@bitrix24/b24icons-vue/actions/Conversion1Icon'
import AchievementIcon from '@bitrix24/b24icons-vue/outline/AchievementIcon'

// Импорт иконок для группы Закупки
import ShoppingCartIcon from '@bitrix24/b24icons-vue/outline/ShoppingCartIcon'
import LetterSortDownIcon from '@bitrix24/b24icons-vue/outline/LetterSortDownIcon'
import CalendarIcon from '@bitrix24/b24icons-vue/outline/CalendarIcon'
import MoneyIcon from '@bitrix24/b24icons-vue/outline/MoneyIcon'

// Импорт иконок для группы Достижения
import DealIcon from '@bitrix24/b24icons-vue/crm/DealIcon'
import ClockIcon from '@bitrix24/b24icons-vue/outline/ClockIcon'
import SmileIcon from '@bitrix24/b24icons-vue/outline/SmileIcon'
import HeadsetIcon from '@bitrix24/b24icons-vue/outline/HeadsetIcon'

// Группы карточек
const reportGroups = [
  {
    id: 'sales',
    title: 'Продажи',
    reports: [
      {
        id: 'sales-monthly',
        title: 'Анализ продаж по месяцам',
        description: 'Динамика продаж по месяцам с детализацией по продуктам',
        icon: GraphsDiagramIcon,
        to: '#'
      },
      {
        id: 'sales-funnel',
        title: 'Воронка продаж',
        description: 'Конверсия на каждом этапе воронки продаж',
        icon: Funnel1Icon,
        to: '#'
      },
      {
        id: 'lead-conversion',
        title: 'Конверсия лидов',
        description: 'Эффективность конвертации лидов в клиентов',
        icon: Conversion1Icon,
        to: '#'
      },
      {
        id: 'top-managers',
        title: 'Топ менеджеры',
        description: 'Рейтинг менеджеров по объемам продаж',
        icon: AchievementIcon,
        to: '#'
      }
    ]
  },
  {
    id: 'purchases',
    title: 'Закупки',
    reports: [
      {
        id: 'purchase-analysis',
        title: 'Анализ закупок',
        description: 'Объемы закупок по категориям и периодам',
        icon: ShoppingCartIcon,
        to: '#'
      },
      {
        id: 'supplier-comparison',
        title: 'Сравнение поставщиков',
        description: 'Сравнительный анализ поставщиков по цене и качеству',
        icon: LetterSortDownIcon,
        to: '#'
      },
      {
        id: 'delivery-terms',
        title: 'Сроки поставок',
        description: 'Соблюдение сроков поставок и задержки',
        icon: CalendarIcon,
        to: '#'
      },
      {
        id: 'purchase-budget',
        title: 'Бюджет закупок',
        description: 'Расходы на закупки и планирование бюджета',
        icon: MoneyIcon,
        to: '#'
      }
    ]
  },
  {
    id: 'achievements',
    title: 'Достижения',
    reports: [
      {
        id: 'kpi-performance',
        title: 'Выполнение KPI',
        description: 'Отчет по выполнению ключевых показателей эффективности',
        icon: DealIcon,
        to: '#'
      },
      {
        id: 'employee-rankings',
        title: 'Рейтинги сотрудников',
        description: 'Сравнительные рейтинги по отделам и должностям',
        icon: ClockIcon,
        to: '#'
      },
      {
        id: 'goal-progress',
        title: 'Прогресс по целям',
        description: 'Достижение квартальных и годовых целей компании',
        icon: SmileIcon,
        to: '#'
      },
      {
        id: 'performance-awards',
        title: 'Награды за результаты',
        description: 'Статистика наград и премий за достижения',
        icon: HeadsetIcon,
        to: '#'
      }
    ]
  }
]

const b24Instance = useB24()
const pageTitle = 'Пример 44'

onMounted(() => {
  const $b24 = b24Instance.get()
  if (b24Instance.isInit() && $b24) {
    $b24.parent.setTitle(pageTitle)
  }
})
</script>

<template>
  <B24DashboardPanel>
    <template #header>
      <B24DashboardNavbar :title="pageTitle">
        <template #right>
          <B24Button size="sm" label="Feedback" />
        </template>
      </B24DashboardNavbar>
    </template>

    <template #body>
      <!-- Группы карточек -->
      <section
        v-for="group in reportGroups"
        :key="group.id"
      >
        <!-- Заголовок группы -->
        <ProseH2>{{ group.title }}</ProseH2>

        <!-- Карточки -->
        <B24PageGrid>
          <B24PageCard
            v-for="report in group.reports"
            :key="report.id"
            v-bind="report"
          />
        </B24PageGrid>
      </section>
    </template>
  </B24DashboardPanel>
</template>