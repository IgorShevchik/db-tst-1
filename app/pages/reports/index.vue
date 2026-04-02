<script setup lang="ts">
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'
import ChartLineIcon from '@bitrix24/b24icons-vue/main/ChartLineIcon'
import FunnelIcon from '@bitrix24/b24icons-vue/outline/FunnelIcon'
import ConversionIcon from '@bitrix24/b24icons-vue/outline/ConversionIcon'
import TrophyIcon from '@bitrix24/b24icons-vue/outline/TrophyIcon'
import DealIcon from '@bitrix24/b24icons-vue/main/DealIcon'
import ClockIcon from '@bitrix24/b24icons-vue/outline/ClockIcon'
import SmileIcon from '@bitrix24/b24icons-vue/outline/SmileIcon'
import HeadphonesIcon from '@bitrix24/b24icons-vue/outline/HeadphonesIcon'
import ShoppingCartIcon from '@bitrix24/b24icons-vue/main/ShoppingCartIcon'
import CompareIcon from '@bitrix24/b24icons-vue/outline/CompareIcon'
import CalendarIcon from '@bitrix24/b24icons-vue/outline/CalendarIcon'
import MoneyIcon from '@bitrix24/b24icons-vue/outline/MoneyIcon'
import { useB24 } from '~/composables/useB24'

// Группы отчетов с данными
const reportGroups = [
  {
    id: 'sales',
    title: 'Продажи',
    icon: ChartLineIcon,
    description: 'Отчеты по анализу продаж и эффективности',
    reports: [
      {
        id: 'sales-monthly',
        title: 'Анализ продаж по месяцам',
        description: 'Динамика продаж по месяцам с детализацией по продуктам',
        icon: ChartLineIcon,
        to: '/reports/sales/monthly'
      },
      {
        id: 'sales-funnel',
        title: 'Воронка продаж',
        description: 'Конверсия на каждом этапе воронки продаж',
        icon: FunnelIcon,
        to: '/reports/sales/funnel'
      },
      {
        id: 'lead-conversion',
        title: 'Конверсия лидов',
        description: 'Эффективность конвертации лидов в клиентов',
        icon: ConversionIcon,
        to: '/reports/sales/conversion'
      },
      {
        id: 'top-managers',
        title: 'Топ менеджеры',
        description: 'Рейтинг менеджеров по объемам продаж',
        icon: TrophyIcon,
        to: '/reports/sales/top-managers'
      }
    ]
  },
  {
    id: 'support',
    title: 'Сопровождение',
    icon: HeadphonesIcon,
    description: 'Отчеты по клиентскому обслуживанию и поддержке',
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
        icon: HeadphonesIcon,
        to: '/reports/support/efficiency'
      }
    ]
  },
  {
    id: 'purchases',
    title: 'Закупки',
    icon: ShoppingCartIcon,
    description: 'Отчеты по закупочной деятельности и поставщикам',
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
        icon: CompareIcon,
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

// Для установки заголовка в Bitrix24
const { t } = useI18n()
const b24Instance = useB24()
const router = useRouter()
const pageTitle = 'Отчеты'

onMounted(() => {
  const $b24 = b24Instance.get()
  if (b24Instance.isInit() && $b24) {
    $b24.parent.setTitle(pageTitle)
  }
})
</script>

<template>
  <B24DashboardPanel id="reports" :b24ui="{ body: 'p-6' }">
    <template #header>
      <B24DashboardNavbar :title="pageTitle">
        <template #right>
          <B24Button
            size="sm"
            label="Экспорт всех отчетов"
            color="air-secondary"
          />
        </template>
      </B24DashboardNavbar>

      <B24DashboardToolbar>
        <template #left>
          <B24Button
            label="Обновить данные"
            color="air-secondary"
            loading-auto
          />
          <B24Button
            label="Настроить отчеты"
            color="air-tertiary"
          />
        </template>
      </B24DashboardToolbar>
    </template>

    <template #body>
      <div class="space-y-8">
        <!-- Группы отчетов -->
        <div
          v-for="group in reportGroups"
          :key="group.id"
          class="space-y-4"
        >
          <!-- Заголовок группы -->
          <div class="flex items-center gap-3">
            <component
              :is="group.icon"
              class="size-8 text-air-primary"
            />
            <div>
              <h2 class="text-2xl font-semibold text-default">
                {{ group.title }}
              </h2>
              <p class="text-sm text-muted">
                {{ group.description }}
              </p>
            </div>
          </div>

          <!-- Карточки отчетов -->
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <B24Card
              v-for="report in group.reports"
              :key="report.id"
              :b24ui="{
                base: 'h-full hover:shadow-lg transition-shadow duration-200 cursor-pointer',
                body: 'p-4 flex flex-col items-center text-center'
              }"
              @click="router.push(report.to)"
            >
              <template #body>
                <!-- Иконка отчета -->
                <div class="mb-3 p-3 rounded-full bg-air-primary/10">
                  <component
                    :is="report.icon"
                    class="size-6 text-air-primary"
                  />
                </div>

                <!-- Заголовок отчета -->
                <h3 class="font-medium text-default mb-2 line-clamp-2">
                  {{ report.title }}
                </h3>

                <!-- Описание отчета -->
                <p class="text-xs text-muted mb-4 line-clamp-3 flex-grow">
                  {{ report.description }}
                </p>

                <!-- Ссылка -->
                <B24Button
                  size="xs"
                  color="air-tertiary"
                  label="Открыть отчет"
                  :b24ui="{ base: 'w-full' }"
                  @click.stop="router.push(report.to)"
                />
              </template>
            </B24Card>
          </div>
        </div>
      </div>

      <!-- Быстрые действия -->
      <div class="mt-12 pt-8 border-t border-muted">
        <h3 class="text-lg font-medium text-default mb-4">
          Быстрые действия
        </h3>
        <div class="flex flex-wrap gap-3">
          <B24Button
            label="Создать новый отчет"
            color="air-primary"
            :icon="ChartLineIcon"
          />
          <B24Button
            label="Настроить шаблоны"
            color="air-secondary"
          />
          <B24Button
            label="Расписание отчетов"
            color="air-tertiary"
          />
        </div>
      </div>
    </template>
  </B24DashboardPanel>
</template>
