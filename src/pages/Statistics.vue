<template>
  <q-page class="statistics-page">
    <div class="row filters">
      <q-btn-dropdown
        class="datepicker"
        label="4.01.21 - 10.01.21"
        :ripple="false"
      >
        <div class="datepicker-menu">
          <div class="datepicker-list">
            <div class="datepicker-listitem">Сегодня</div>
            <div class="datepicker-listitem">Вчера</div>
            <div class="datepicker-listitem">Позавчера</div>
            <div class="datepicker-listitem active">Текущая неделя</div>
            <div class="datepicker-listitem">Прошлая неделя</div>
            <div class="datepicker-listitem">Текущий месяц</div>
            <div class="datepicker-listitem">Прошлый месяц</div>
            <div class="datepicker-listitem">- 7 дней</div>
            <div class="datepicker-listitem">- 30 дней</div>
            <div class="datepicker-listitem">- 90 дней</div>
          </div>

          <q-date v-model="dateOne" minimal range />

          <q-date v-model="dateOne" minimal range />

          <div class="datepicker-btn">Отменить</div>
        </div>
      </q-btn-dropdown>

      <q-btn-dropdown
        class="group"
        label="Группировать по:"
        :ripple="false"
        no-caps
        dropdown-icon="keyboard_arrow_down"
      >
        <q-list>
          <q-item>
            <q-item-section>
              <q-item-label>Photos</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>

      <q-btn-dropdown
        class="filter"
        label="Фильтры"
        :ripple="false"
        no-caps
      >
        <q-list>
          <q-item>
            <q-item-section>
              <q-item-label>Photos</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>

      <q-btn class="btn" :ripple="false" label="Показать" unelevated no-caps />

      <q-toggle class="graphic-toggle" v-model="graphicToggle" label="График" left-label />

      <div class="cvs-icon">
         <img src="../assets/exportcsv.svg" alt="">
      </div>
    </div>

    <q-markup-table flat>
        <thead>
          <tr>
            <th class="text-left">
              <span>Дата
                <span class="sorting">
                  <img src="../assets/sorting.svg" alt="">
                </span>
              </span>
            </th>
            <th class="text-left">
              <span>Показы
                <span class="sorting">
                  <img src="../assets/sorting.svg" alt="">
                </span>
              </span>
            </th>
            <th class="text-left">
              <span>Клики
                <span class="sorting">
                  <img src="../assets/sorting.svg" alt="">
                </span>
              </span>
            </th>
            <th class="text-left">
              <span>Ун. клики
                <span class="sorting">
                  <img src="../assets/sorting.svg" alt="">
                </span>
              </span>
            </th>
            <th class="text-left">
              <span>CTR
                <span class="sorting">
                  <img src="../assets/sorting.svg" alt="">
                </span>
              </span>
            </th>
            <th class="text-left">
              <span>CPM
                <span class="sorting">
                  <img src="../assets/sorting.svg" alt="">
                </span>
              </span></th>
            <th class="text-right">
              <span>Доход
                <span class="sorting">
                  <img src="../assets/sorting.svg" alt="">
                </span>
              </span>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
          <tr>
            <td class="text-left">01.02.2021</td>
            <td class="text-left">98</td>
            <td class="text-left">58</td>
            <td class="text-left">554</td>
            <td class="text-left">400.66</td>
            <td class="text-left">258.33</td>
            <td class="text-right">380.88 ₽</td>
          </tr>
        </tbody>
    </q-markup-table>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      graphicToggle: false,
      dateOne: { from: '2021/01/04', to: '2021/01/10' },
      dateTwo: ''
    }
  }
};
</script>

<style lang="scss">
.q-page {
  padding: 40px;
}

.statistics-page {
  .filters {
    margin: 0px 0px 40px 0px;
  }

  .q-btn + .q-btn {
    margin: 0px 0px 0px 24px;
  }

  .datepicker {
    color: #12284C;
    border: 1px solid #A0A9B7;
    box-sizing: border-box;
    border-radius: 4px;
    font-size: 16px;
    line-height: 20px;
    letter-spacing: -0.15px;
    position: relative;

    .q-btn__wrapper {
      padding: 10px 15px 8px 63px;
      min-height: 0px;
    }

    .q-focus-helper, i, .q-btn__wrapper:before {
      display: none;
    }

    &::after {
      content:'';
      position: absolute;
      width: 24px;
      height: 24px;
      top: 7px;
      left: 15px;
      background: url('../assets/calendar.svg') 0 0 no-repeat;
    }
  }

  .group {
    color: #A0A9B7;
    border: 1px solid #A0A9B7;
    box-sizing: border-box;
    border-radius: 4px;
    font-size: 16px;
    line-height: 20px;
    letter-spacing: -0.15px;
    position: relative;

    .q-btn__wrapper {
      padding: 10px 15px 8px 16px;
      min-height: 0px;
    }

    .q-focus-helper, .q-btn__wrapper:before {
      display: none;
    }

    .q-btn-dropdown__arrow {
      font-size: 24px;
      margin: -5px -8px -2px 20px;
      color: #4690FF;
    }
  }

  .filter {
    color: #12284C;
    border: 1px solid #A0A9B7;
    box-sizing: border-box;
    border-radius: 4px;
    font-size: 16px;
    line-height: 20px;
    letter-spacing: -0.15px;
    position: relative;

    .q-btn__wrapper {
      padding: 10px 15px 8px 63px;
      min-height: 0px;
    }

    .q-focus-helper, i, .q-btn__wrapper:before {
      display: none;
    }

    &::after {
      content:'';
      position: absolute;
      width: 24px;
      height: 24px;
      top: 7px;
      left: 15px;
      background: url('../assets/filter.svg') 0 0 no-repeat;
    }
  }

  .btn {
    color: #fff;
    background-color: #4690ff;
    font-size: 18px;
    line-height: 22px;
    height: 40px;

    &:hover {
      background: #629df6;
    }

    .q-btn__wrapper {
      min-height: 0;
    }

    &:active {
      background: #4690ff;
      box-shadow: inset 0px 0px 8px rgba(18, 40, 76, 0.48);
    }

    @media (max-width:1360px){
      height: 38px;
      font-size: 16px;
      line-height: 20px;
    }
  }

  .graphic-toggle {
    margin: 0px 0px 0px auto;

    .q-toggle__track {
      height: 24px;
      width: 40px;
      border-radius: 500px;
      opacity: 0.38;
      background: transparent;
      border: 1px solid #5a6577;
    }

    .q-toggle__label {
      font-size: 16px;
      color: #12284C;
    }

    .q-toggle__inner {
      font-size: 40px;
      margin: 0px 0 0 10px;
      width: 40px;
      min-width: 0;
      height: 40px;
      padding: 8px 0px 9px 6px;
    }

    .q-toggle__inner--truthy {
      .q-toggle__thumb::after {
        background-color: #4690FF;
      }

      .q-toggle__track {
        border: 1px solid #4690FF;
      }
    }

    .q-toggle__thumb {
      width: 16px;
      height: 16px;
    }

    .q-toggle__thumb::after {
      background: #A0A9B7;
      width: 16px;
      height: 16px;
      top: 2px;
      box-shadow: none;
    }

    .q-toggle__thumb:before {
      display: none;
    }
  }

  .cvs-icon {
    cursor: pointer;
    display: flex;
    margin: 0px 0px 0px 54px;
  }

  .q-markup-table {
    box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
    border-radius: 4px;

    .q-table {
      padding: 24px 24px 9px;
      width: 0;

      thead {
        tr {
          height: 0px;
        }

        th {
          padding: 3px 0 18px 0px;
          font-size: 18px;
          line-height: 18px;
          color: #596982;
          letter-spacing: 0.03em;
          min-width: 240px;

          span {
            cursor: pointer;
            display: inline-block;
            position: relative;
            padding: 0px 35px 0px 0px;
          }

          .sorting {
            position: absolute;
            width: 24px;
            height: 24px;
            top: -3px;
            right: -11px;
          }
        }

        .text-right {
          min-width: 96px;
        }
      }

      tbody {
        tr {

        }

        td {
          font-size: 18px;
          line-height: 22px;
          padding: 16px 0px 15px 0px;
          height: 54px;
          min-width: 240px;

          &:before {
            background: transparent
          }
        }

        .text-right {
          min-width: 96px;
          color: #95BD5A;
          padding: 0px 16px 0px 0px;
        }

      }
    }
  }
}

.q-menu {
  .datepicker-list {
    margin: 1px 48px 0px 0px;
    padding: 0px 0px 17px 0px;
    min-width: 140px;

    .datepicker-listitem {
      cursor: pointer;
      font-size: 14px;
      line-height: 17px;
      color: #596982;
      position: relative;

      & + .datepicker-listitem {
        margin: 25px 0px 0px 0px;
      }

      &.active{
        color: #4690FF;

        &::after {
          content:'';
          position: absolute;
          width: 2px;
          height: 18px;
          top: 0;
          right: -2px;
          background-color: #4690FF;
        }
      }

    }
  }

  .datepicker-menu {
    display: flex;
    position: relative;

    padding: 40px;

    .q-date {
      & + .q-date {
        margin: 0px 0px 0px 40px;
      }

      box-shadow: none;
      min-width: 322px;

      &__navigation {
        height: 17px;
        margin: 0px 0px 32px 0px;
      }

      &__calendar-weekdays {
        height: 46px;
      }

      &__header, &__actions {
        display: none;
      }

      &__view, &__calendar-days-container {
        min-height: 0;
      }

      &__view {
        padding: 0;
      }

      &__calendar-item {
        font-weight: 500;
        font-size: 14px;
        line-height: 17px;
        opacity: 1;
        color: #12284C;

        .q-focus-helper {
          // display: none;
        }

        &--in {
          font-weight: 400;
        }

        .block {
          color: #12284C;
        }
      }

      &__calendar-days > div {
        height: 46px !important;
        width: 46px !important;
      }

      &__edit-range {
        background-color: #4690FF;
      }

      &__range-from, &__edit-range-from, &__range-to, &__edit-range-to {
        background-color: #4690FF;
        border-radius: 4px;

        .bg-primary {
          background-color: transparent !important;
        }

        .q-focus-helper {
          display: none;
        }

        .block {
          color: #fff;
        }
      }

      &__range-from:before, &__range-to:before {
        display: none;
      }

      &__range:before {
        background: #d4e4fe;
      }

      &__months-item, &__years-item {
        .block {
          color: #12284C !important;
        }
        .q-btn {
          box-shadow: none !important;
        }
      }
    }

    .datepicker-btn {
      font-weight: 500;
      font-size: 18px;
      line-height: 22px;
      color: #596982;
      cursor: pointer;
      position: absolute;
      bottom: 49px;
      right: 40px;
    }
  }
}
</style>
