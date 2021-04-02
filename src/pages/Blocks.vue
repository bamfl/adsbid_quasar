<template>
  <q-page class="blocks-page">
    <div class="title">Создание блока</div>

    <nav class="nav">
      <div class="steps">
        <div class="step active">
          <div class="number">1</div>
          <span>Общие</span>
        </div>
        <div class="step">
          <div class="number">2</div>
          <span>Шаблоны (A/B тест)</span>
        </div>
        <div class="step">
          <div class="number">3</div>
          <span>Выбор сайтов</span>
        </div>
      </div>

      <div class="buttons">
        <q-btn class="btn btn-grey" :ripple="false" label="Перейти сразу к выбору сайтов" unelevated no-caps />
        <q-btn class="btn btn-blue" :ripple="false" label="Далее" unelevated no-caps />
      </div>
    </nav>

    <q-card>
      <q-tabs v-model="tab" align="left">
        <q-tab
          :ripple="false"
          name="fastSettings"
          label="Быстрая настройка"
          no-caps
        ></q-tab>
        <q-tab
          :ripple="false"
          name="wideSettings"
          label="Расширенные настройки"
          no-caps
        ></q-tab>

        <div class="device">
          <div class="pc active">
            <svg width="22" height="18" viewBox="0 0 22 18" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M21.1851 16.4149H0.81481C0.365035 16.4149 0 16.7699 0 17.2074C0 17.6448 0.365035 17.9998 0.81481 17.9998H21.1851C21.6348 17.9998 21.9999 17.6448 21.9999 17.2074C21.9999 16.7699 21.6348 16.4149 21.1851 16.4149ZM12.2731 7.35146C12.2731 6.66878 11.7019 6.11328 10.9999 6.11328C10.298 6.11328 9.72679 6.66878 9.72679 7.35146V8.44106H12.2731V7.35146Z" fill="#4690FF"/>
            <path d="M3.25915 13.4714H18.7405C19.1903 13.4714 19.5553 13.1164 19.5553 12.679V0.792435C19.5553 0.355011 19.1903 0 18.7405 0H3.25915C2.80937 0 2.44434 0.355011 2.44434 0.792435V12.679C2.44434 13.1164 2.80937 13.4714 3.25915 13.4714Z" fill="#4690FF"/>
            </svg>
          </div>
          <div class="mob">
            <svg width="12" height="22" viewBox="0 0 12 22" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 2.05555V0.888887C12 0.674221 11.8212 0.5 11.6 0.5H0.399998C0.179199 0.5 0 0.674221 0 0.888887V2.05555H12Z" fill="#596982"/>
            <path d="M12 2.83301H0V17.6108H12V2.83301Z" fill="#596982"/>
            <path d="M0 18.3887V21.1109C0 21.3259 0.179199 21.4998 0.399998 21.4998H11.6C11.8212 21.4998 12 21.3259 12 21.1109V18.3887H0ZM5.99998 20.3331C5.55838 20.3331 5.19998 19.9847 5.19998 19.5553C5.19998 19.126 5.55838 18.7776 5.99998 18.7776C6.44157 18.7776 6.79997 19.126 6.79997 19.5553C6.79997 19.9847 6.44157 20.3331 5.99998 20.3331Z" fill="#596982"/>
            </svg>
          </div>
        </div>
      </q-tabs>

      <q-tab-panels v-model="tab">
        <q-tab-panel name="fastSettings">
          <div class="row">
            <div class="card settings">
              <div class="item">
                <div class="item__name">Название блока</div>
                <div class="item__text">31.03.2021_11:12:44</div>
              </div>

              <div class="item">
                <div class="item__name">Категория объявлений</div>
                <div class="item__buttons">
                  <div class="item__btn">Все</div>
                  <div class="item__btn">Товары</div>
                  <div class="item__btn">Новости</div>
                </div>
              </div>

              <div class="item">
                <div class="item__name">Рейтинг объявлений <span>i</span></div>
                <q-select
                  filled
                  v-model="filterSites"
                  input-debounce="0"
                  :label="optionsOne[0]"
                  :options="optionsOne"
                  style="height: 40px"
                  dropdown-icon="keyboard_arrow_down"
                  popup-content-class="filterSites"
                  behavior="menu"
                  menu-anchor="bottom left"
                  menu-self="top left"
                  :menu-offset="[1, -10]"
                >
                </q-select>
              </div>

              <div class="item">
                <div class="item__name">Форма блока</div>
                <div class="forms">
                  <div class="forms__header"></div>
                  <div class="forms__content"></div>
                  <div class="forms__aside"></div>
                  <div class="forms__footer"></div>
                </div>
              </div>

              <div class="item">
                <div class="item__name">Шаблоны</div>
                <ul class="item__list">
                  <li>Горизонтальный 1</li>
                  <li>Горизонтальный 2</li>
                  <li>Большой</li>
                  <li>Графический 1</li>
                  <li>Карусель</li>
                  <li>Вертикальный 1</li>
                  <li>Графический 2</li>
                  <li>Горизонтальный 3</li>
                  <li>Графический 3</li>
                  <li>Объявления с датой публикации</li>
                  <li>Горизонтальный 4</li>
                  <li>Социальный</li>
                  <li>Вертикальный 2</li>
                  <li>Вьетнамский с размытием</li>
                  <li>Графический 4</li>
                  <li>Горизонтальный 5</li>
                  <li>Блок с узким тизером</li>
                  <li>Графический с кнопкой "Читать"</li>
                </ul>
              </div>

              <div class="item">
                <div class="item__name">Количество тизеров</div>

                <div class="item__ranges">
                  <div class="item__range">
                    <q-slider v-model="rows" :min="0" :max="10" label label-always />
                    <span>По горизонтали</span>
                  </div>
  
                  <div class="item__range">
                    <q-slider v-model="columns" :min="0" :max="10" label label-always />
                    <span>По вертикали</span>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="card blocks">
              <div class="blocks__head">
                <div class="blocks__fullscreen">
                  <svg width="22" height="22" viewBox="0 0 22 22" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M22 0V8.24725L19.2514 5.49725L15.1277 9.62225L12.3777 6.875L16.5028 2.74175L13.7527 0H22V0ZM6.87775 12.3723L2.75137 16.4972L0 13.7473V22H8.25275L5.50275 19.2555L9.62775 15.125L6.87775 12.3723ZM15.125 12.3777L12.3777 15.1277L16.5028 19.2528L13.7527 22H22V13.7527L19.2582 16.5028L15.125 12.3777ZM8.25275 0H0V8.25275L2.7445 5.50275L6.875 9.62775L9.62775 6.87775L5.50275 2.75275L8.25275 0Z" fill="#596982"/>
                  </svg>
                </div>
                <q-btn class="btn btn-red" :ripple="false" label="Сбросить все" unelevated no-caps />
              </div>
            </div>
          </div>
        </q-tab-panel>

        <q-tab-panel name="wideSettings">
          <span>Расширенные настройки</span>
        </q-tab-panel>
      </q-tab-panels>
    </q-card>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      tab: "fastSettings",
      filterSites: null,
      optionsOne: [
        "Рейтинг 1 <br> (Объявления вызывающего характера, <br>  в том числе с <br> рекламой тематикой: <br>  мужское/женское здоровье)","Рейтинг 2 <br> (Объявления умеренного <br> содержания, но допускается реклама <br>  мужского/женского здоровья)",
        "Рейтинг 3 <br> (Объявления умеренного содержания)"
      ],
      rows: 6,
      columns: 6
    }
  }
}
</script>

<style lang="scss">
  .q-page {
    padding: 40px 40px 0;

    @media (max-width:1600px){
      padding: 32px 40px 0 !important;
    }

    @media (max-width:1360px){
      padding: 32px 32px 0 !important;
    }
  }

  .blocks-page {
    .title {
      font-weight: 500;
      font-size: 18px;
      line-height: 22px;
      color: #12284C;
      margin: 0px 0px 32px 0px;
    }

    .nav {
      display: flex;
      justify-content: space-between;
      margin: 0px 0px 37px 0px;

      .steps {
        display: flex;

        .step {
          font-weight: 500;
          font-size: 14px;
          line-height: 17px;
          margin: 0px 32px 0px 0px;
          cursor: pointer;          

          .number {
            background: #A0A9B7;
            margin: 0 auto 5px;
            color: #fff;
            border-radius: 4px;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 24px;
            height: 24px;
          }

          span {
            color: #A0A9B7;
          }

          &:last-child {
            margin: 0;
          }

          &.active {
            .number {
              background: #4690FF;
            }

            span {
              color: #12284C;
            }
          }
        }
      }
    }

    .buttons {
      .btn {
        color: #fff;
        background-color: #4690ff;
        font-size: 18px;
        line-height: 22px;
        height: 40px;
        margin: 3px 48px 0px 0px;

        &:last-child {
          margin: 0;
        }

        &:hover {
          background: #629df6;
        }

        .q-focus-helper {
          display: none;
        }

        .q-btn__wrapper {
          min-height: 0;
          z-index: 1;
        }

        &:active {
          background: #4690ff;
          box-shadow: inset 0px 0px 8px rgba(18, 40, 76, 0.48);
        }

        &-grey {
          color: #596982;
          background-color: #fff;
          transition: all 0.3s;

          .q-btn__wrapper {
            padding: 0;
          }

          &:hover,
          &:active {
            box-shadow: none;
            background-color: #fff;
            color: #12284c;
          }
        }
      }
    }

    .q-card {
      box-shadow: none;
      position: relative;
    }

    .q-tabs {
      display: flex;
      margin: 0px 0px 32px 0px;
      padding: 3px 0px 0px 0px;

      .device {
        display: flex;
        align-items: center;
        margin: 0px 0px 0px auto;

        .pc {
          margin: 2px 31px 0px 0px;
        }

        .mob {
          margin: 2px 6px 0px 0px;
        }

        .pc, .mob {
          cursor: pointer;
          &.active{
            svg {
              path {
                fill: #4690FF;
              }
            }            
          }
        }
      }
    }

    .q-tab {
      outline: none;
      flex: 0 1 auto;
      cursor: pointer;
      padding: 0;
      margin: 0;
      min-height: 0;
      padding: 0px 0px 2px 0px;

      .q-focus-helper {
        display: none;
      }

      &-panel {
        padding: 0;

        .label {
          font-size: 12px;
          line-height: 15px;
          color: #12284C;
          display: flex;
          justify-content: space-between;
          margin: 0px 0px 8px 0px;
        }

        .q-field {
          border: 1px solid #A0A9B7;
          border-radius: 4px;
          height: 40px;
          overflow: hidden;
          margin: 0px 0px 24px 0px;

          &.quantity {
            max-width: 116px;
          }

          &__control {
            height: 40px;
            min-height: 0;
            padding: 0px;
            background-color: transparent;

            &::before {
              display: none;
            }
          }

          &__control-container {
            padding-top: 0;
          }

          &--float {
            .q-field__label {
              display: none;
            }
          }

          &__native {
            padding: 9px 16px 7px 16px;
            font-size: 16px;
            line-height: 20px;
            letter-spacing: -0.1px;

            @media (max-width:600px){
              font-size: 14px;
            }
          }

          .q-select__dropdown-icon {
            font-size: 24px;
            margin: -18px 7px 0px 0px;
            color: #4690ff;
          }

          &__label {
            font-size: 16px;
            line-height: 20px;
            letter-spacing: 0;
            top: 10px;
            left: 15px;

            @media (max-width:600px){
              font-size: 14px;
            }
          }
        }

        .search {
          margin: 0px 0px 16px 0px;
          position: relative;

          &::before {
            content:'';
            position: absolute;
            width: 24px;
            height: 24px;
            top: 9px;
            left: 17px;
            background: url('../assets/search.svg') 0 0 no-repeat;
          }

          .q-field {
            &__native {
              padding: 9px 16px 7px 64px;
              font-size: 16px;
              line-height: 20px;
              letter-spacing: -0.1px;

              @media (max-width:1360px){
                padding: 8px 16px 7px 52px;
                font-size: 14px;
                line-height: 17px ;
              }
            }
          }
        }

        .quantity {
          .q-field {
            &__native {
              padding: 9px 16px 7px 16px;
              font-size: 16px;
              line-height: 20px;
              letter-spacing: -0.1px;

              @media (max-width:600px){
                font-size: 14px;
              }
            }
          }
        }

        .domain__list {
          list-style: none;
          padding: 0;
          margin: 0;

          li {
            & + li {
              margin: 9px 0px 0px 0px;
            }

            &:last-child {
              margin: 9px 0px 32px 0px;
            }

            .q-checkbox {
              width: 22px;
              height: 22px;
              margin: 9px 23px 0px 1px;

              &__inner {
                font-size: 22px;
                width: 22px;
                min-width: 22px;
                height: 22px;
                outline: 0;
                border-radius: 50%;
                color: #596982;

                &::before {
                  content:'';
                  display: none;
                }

                &--truthy {
                  .q-checkbox__svg {
                    color: #12284C;

                    path {
                      fill: #fff;
                    }

                    &.absolute-full {
                      top: -4px;
                      transform: translate(2px, 0);
                    }
                  }

                  .q-checkbox__bg {
                    color: #fff;
                    border: 2px solid #12284C;
                    position: relative;
                    svg {
                      z-index: 1;
                    }

                    &::after {
                      content:'';
                      position: absolute;
                      width: 7px;
                      height: 7px;
                      top: -2px;
                      right: -2px;
                      background-color: #fff;
                      z-index: 0;
                    }
                  }
                }
              }

              &__bg {
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
              }

              &__label {
                margin: 0px 0px 0px 17px;
              }
            }
          }
        }
      }

      &-panels {
        .scroll {
          overflow: visible;
        }
      }

      &__label {
        color: #596982;
        font-size: 18px;
        line-height: 25px;
        letter-spacing: -0.1px;

        &:hover{
          color: #12284C !important;
        }

        @media (max-width:1360px){
          font-size: 16px !important;
          line-height: 20px;
        }
      }

      & + .q-tab {
        margin: 0px 0px 0px 22px;

        @media (max-width:1360px){
          margin: 0px 0px 0px 24px;
        }
      }

      &--active {
        position: relative;

        .q-tab__label {
          color: #12284C !important;


        }

        &::after {
          content: "";
          position: absolute;
          width: 100%;
          height: 100%;
          top: 0px;
          left: 0;
          border-bottom: 2px solid #4690ff;
        }
      }

      &__indicator {
        display: none;
      }

      &__content {
        padding: 0;
        min-width: 0;
      }
    }

    .q-panel-parent {
      overflow: visible;
    }

    .row {
      .card {
        box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
        border-radius: 4px;
        padding: 32px 40px 30px;
        height: 100%;
      }

      .settings {
        flex: 0 1 460px;
        margin: 0px 40px 0px 0px;

        .item {
          margin: 1px 0px 24px 0px;

          &__name {
            font-weight: 500;
            font-size: 14px;
            line-height: 17px;
            color: #A0A9B7;
            margin: 0px 0px 16px 0px;
          }

          &__text, &__btn {
            font-size: 16px;
            line-height: 20px;
            color: #12284C;
          }

          &__buttons {
            display: flex;
          }

          &__btn {
            padding: 9px;
            border: 1px solid #A0A9B7;
            border-radius: 4px;
            margin: 0px 12px 0px 0px;
            cursor: pointer;

            &:last-child {
              margin: 0;
            }
          }

          &__list {
            list-style: none;
            padding: 0;
            margin: 0;
            max-height: 300px;
            overflow: auto;
            padding: 0px 40px 0px 0px;

            &::-webkit-scrollbar {
              width: 6px;
            }
            
            &::-webkit-scrollbar-thumb {
              background-color: #A0A9B7;
              outline: 1px solid #fff;
              border-radius: 1px;
            }

            li {
              font-size: 16px;
              line-height: 20px;
              color: #12284C;
              padding: 9px 0;
              border: 1px solid #A0A9B7;
              border-radius: 4px;
              margin: 0px 0px 12px 0px;
              text-align: center;
              cursor: pointer;

              &:last-child {
                margin: 0;
              }
            }
          }

          &__ranges {
            display: flex;
            justify-content: space-between;
            margin: 30px -8px 0
          }

          &__range {
            flex: 0 1 50%;
            padding: 0 8px;

            span {
              font-weight: 500;
              font-size: 12px;
              line-height: 18px;
              color: #A0A9B7;
              display: flex;
              justify-content: center;
            }

            .q-slider--h {
              height: 27px;
            }

            .q-slider__track-container {
              background: #12284c15;
            }

            .q-slider__track {
              color: #4690FF;
            }

            .q-slider__pin-text-container {
              transform: translateX(0px) !important;
              transform: translateY(10px) !important;
              right: -40% !important;
            }

            .q-slider__thumb {
              display: none;
            }

            .q-slider__thumb-container {
              width: 6px;
              height: 16px;
              background: #4690FF;
              transform: translate(0px, 2px);

              svg {
                width: 6px;
                height: 16px;

                path {
                  fill: #4690FF;
                }
              }

              .q-slider__focus-ring {
                display: none;
              }

              .q-slider__pin-text {
                font-size: 14px;
                line-height: 18px;
                color: #12284C;
              }
            }
          }

          &:last-child {
            margin: 0;
          }
        }

        .forms {
          display: grid;
          height: 300px;
          max-width: 100%;

          &__header {
            padding: 8px;
            margin-bottom: 4px;
            margin-right: 4px;
            -ms-grid-column: 1;
            grid-column-start: 1;
            -ms-grid-column-span: 10;
            grid-column-end: 10;
            -ms-grid-row: 1;
            grid-row-start: 1;
            -ms-grid-row-span: 4;
            grid-row-end: 4;
            background: url('../assets/header.svg') center / cover no-repeat;
          }

          &__content {
            padding: 8px;
            -ms-grid-column: 1;
            grid-column-start: 1;
            -ms-grid-column-span: 9;
            grid-column-end: 10;
            -ms-grid-row: 4;
            grid-row-start: 4;
            -ms-grid-row-span: 8;
            grid-row-end: 12;
            margin-top: 4px;
            margin-right: 4px;
            margin-bottom: 4px;
            background: url('../assets/content.svg') center / cover no-repeat;
          }

          &__aside {
            padding: 8px;
            -ms-grid-column: 10;
            grid-column-start: 10;
            -ms-grid-column-span: 2;
            grid-column-end: 12;
            -ms-grid-row: 1;
            grid-row-start: 1;
            -ms-grid-row-span: 11;
            grid-row-end: 12;
            margin-bottom: 4px;
            margin-left: 4px;
            background: url('../assets/aside.svg') center / cover no-repeat;
          }

          &__footer {
            padding: 8px;
            -ms-grid-column: 1;
            grid-column-start: 1;
            -ms-grid-column-span: 11;
            grid-column-end: 12;
            -ms-grid-row: 12;
            grid-row-start: 12;
            -ms-grid-row-span: 3;
            grid-row-end: 15;
            margin-top: 4px;
            background: url('../assets/footer.svg') center / cover no-repeat;
          }

          &__header, &__content, &__aside, &__footer {
            border: 1px solid #A0A9B7;
            border-radius: 4px;

            &.active, &:hover{
              border: 1px solid transparent;
              background-color: #f0f5fd;            
            } 
          }
        }
      }

      .blocks {
        flex: 1 1 auto;

        &__head {
          display: flex;
          justify-content: space-between;
          align-items: center;
        }

        &__fullscreen {
          cursor: pointer;
        }

        .btn {
          color: #fff;
          font-size: 18px;
          line-height: 22px;
          height: 40px;
          font-weight: 500;
          transition: 0.3s all;

          .q-focus-helper {
            display: none;
          }

          &:hover {
            background: #629df6;
          }

          .q-btn__wrapper {
            min-height: 0;
            z-index: 9000;
          }


          &:active {
            background: #4690ff;
            box-shadow: inset 0px 0px 8px rgba(18, 40, 76, 0.48);
          }

          &-red {
            color: #b36f6c;
            background-color: #fff;

            .q-btn__wrapper {
              padding: 0;
            }

            &:hover,
            &:active {
              background-color: #fff;
              color: #a64541;
              box-shadow: none;
            }
          }
        }
      }
    }
  }
</style>