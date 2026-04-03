<script setup lang="ts">
import { onMounted } from 'vue'
import { useB24 } from '~/composables/useB24'
import GraphsDiagramIcon from '@bitrix24/b24icons-vue/main/GraphsDiagramIcon'
import Funnel1Icon from '@bitrix24/b24icons-vue/crm/Funnel1Icon'
import Conversion1Icon from '@bitrix24/b24icons-vue/actions/Conversion1Icon'
import AchievementIcon from '@bitrix24/b24icons-vue/outline/AchievementIcon'
import DealIcon from '@bitrix24/b24icons-vue/crm/DealIcon'
import ClockIcon from '@bitrix24/b24icons-vue/outline/ClockIcon'
import SmileIcon from '@bitrix24/b24icons-vue/outline/SmileIcon'
import HeadsetIcon from '@bitrix24/b24icons-vue/outline/HeadsetIcon'
import ShoppingCartIcon from '@bitrix24/b24icons-vue/outline/ShoppingCartIcon'
import LetterSortDownIcon from '@bitrix24/b24icons-vue/outline/LetterSortDownIcon'
import CalendarIcon from '@bitrix24/b24icons-vue/outline/CalendarIcon'
import MoneyIcon from '@bitrix24/b24icons-vue/outline/MoneyIcon'

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
        to: '/reports/sales/monthly'
      },
      {
        id: 'sales-funnel',
        title: 'Воронка продаж',
        description: 'Конверсия на каждом этапе воронки продаж',
        icon: Funnel1Icon,
        to: '/reports/sales/funnel'
      },
      {
        id: 'lead-conversion',
        title: 'Конверсия лидов',
        description: 'Эффективность конвертации лидов в клиентов',
        icon: Conversion1Icon,
        to: '/reports/sales/conversion'
      },
      {
        id: 'top-managers',
        title: 'Топ менеджеры',
        description: 'Рейтинг менеджеров по объемам продаж',
        icon: AchievementIcon,
        to: '/reports/sales/top-managers'
      }
    ]
  },
  {
    id: 'support',
    title: 'Сопровождение',
    reports: [
      {
        id: 'deal-statuses',
        title: 'Статусы сделок',
        description: 'Распределение сделок по текущим статусам',
        icon: DealIcon,
        to: '/reports/support/deal-statuses'
      },
      {
        id: 'response-time',
        title: 'Время реакции на заявки',
        description: 'Среднее время ответа на клиентские обращения',
        icon: ClockIcon,
        to: '/reports/support/response-time'
      },
      {
        id: 'client-satisfaction',
        title: 'Удовлетворенность клиентов',
        description: 'NPS и оценка качества обслуживания',
        icon: SmileIcon,
        to: '/reports/support/client-satisfaction'
      },
      {
        id: 'support-efficiency',
        title: 'Эффективность поддержки',
        description: 'Количество решенных обращений и время решения',
        icon: HeadsetIcon,
        to: '/reports/support/efficiency'
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
        to: '/reports/purchases/analysis'
      },
      {
        id: 'supplier-comparison',
        title: 'Сравнение поставщиков',
        description: 'Сравнительный анализ поставщиков по цене и качеству',
        icon: LetterSortDownIcon,
        to: '/reports/purchases/supplier-comparison'
      },
      {
        id: 'delivery-terms',
        title: 'Сроки поставок',
        description: 'Соблюдение сроков поставок и задержки',
        icon: CalendarIcon,
        to: '/reports/purchases/delivery-terms'
      },
      {
        id: 'purchase-budget',
        title: 'Бюджет закупок',
        description: 'Расходы на закупки и планирование бюджета',
        icon: MoneyIcon,
        to: '/reports/purchases/budget'
      }
    ]
  }
]

const b24Instance = useB24()
const pageTitle = `${0}`

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
