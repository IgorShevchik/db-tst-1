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
        title: 'Ежемесячный отчет по продажам',
        description: 'Детальный анализ продаж по месяцам с разбивкой по регионам и продуктам',
        icon: GraphsDiagramIcon,
        to: '/reports/sales/monthly'
      },
      {
        id: 'sales-customer-base',
        title: 'Анализ клиентской базы',
        description: 'Сегментация клиентов, частота покупок, удержание и отток',
        icon: Funnel1Icon,
        to: '/reports/sales/customer-base'
      },
      {
        id: 'sales-forecast',
        title: 'Прогноз продаж на квартал',
        description: 'Прогнозирование объемов продаж на основе исторических данных и трендов',
        icon: Conversion1Icon,
        to: '/reports/sales/forecast'
      },
      {
        id: 'sales-campaigns',
        title: 'Эффективность рекламных кампаний',
        description: 'ROI рекламных активностей, конверсия и стоимость привлечения клиента',
        icon: AchievementIcon,
        to: '/reports/sales/campaigns'
      }
    ]
  },
  {
    id: 'support',
    title: 'Сопровождение',
    reports: [
      {
        id: 'support-requests',
        title: 'Отчет по обращениям клиентов',
        description: 'Количество обращений, типы проблем, среднее время ответа',
        icon: DealIcon,
        to: '/reports/support/requests'
      },
      {
        id: 'support-resolution',
        title: 'Время решения задач',
        description: 'Анализ времени на решение задач и удовлетворенность клиентов',
        icon: ClockIcon,
        to: '/reports/support/resolution'
      },
      {
        id: 'support-csi',
        title: 'Удовлетворенность клиентов (CSI)',
        description: 'Индекс удовлетворенности клиентов на основе опросов и отзывов',
        icon: SmileIcon,
        to: '/reports/support/csi'
      },
      {
        id: 'support-workload',
        title: 'Загрузка службы поддержки',
        description: 'Распределение нагрузки между сотрудниками, эффективность работы',
        icon: HeadsetIcon,
        to: '/reports/support/workload'
      }
    ]
  },
  {
    id: 'purchases',
    title: 'Закупки',
    reports: [
      {
        id: 'purchases-price-analysis',
        title: 'Анализ цен поставщиков',
        description: 'Сравнение цен у разных поставщиков, динамика изменения',
        icon: ShoppingCartIcon,
        to: '/reports/purchases/price-analysis'
      },
      {
        id: 'purchases-delivery',
        title: 'Отчет по срокам доставки',
        description: 'Соблюдение сроков поставок, анализ задержек и их причин',
        icon: CalendarIcon,
        to: '/reports/purchases/delivery'
      },
      {
        id: 'purchases-budget',
        title: 'Контроль бюджета закупок',
        description: 'Фактические расходы против плановых, экономия и перерасход',
        icon: MoneyIcon,
        to: '/reports/purchases/budget'
      },
      {
        id: 'purchases-tenders',
        title: 'Тендерная активность',
        description: 'Участие в тендерах, результаты, анализ конкурентов',
        icon: LetterSortDownIcon,
        to: '/reports/purchases/tenders'
      }
    ]
  }
]

const b24Instance = useB24()
const pageTitle = 'Отчеты'

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