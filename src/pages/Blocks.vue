<template>
  <q-page class="blocks-page">
    <div class="title">Создание блока</div>

    <nav class="nav">
      <div class="steps">
        <div class="step active">
          <div class="number">1</div>
          <span>Создание блока</span>
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

        <div class="row">
          <q-tab-panels v-model="tab">
            <q-tab-panel name="fastSettings">
              <div class="card settings">
                <div class="item">
                  <div class="item__name">Название блока</div>

                  <div v-if="blockNameChange" class="item__changename">
                    <q-input outlined v-model="blockName" @keyup.enter="blockNameChange = false" />
                    <div class="actions">
                      <div class="accept" @click="blockNameChange = false">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" clip-rule="evenodd" d="M21.5211 7.85765L11.0976 18.5102C10.4557 19.1632 9.42289 19.1632 8.78184 18.5102L2.48141 12.0266C1.83953 11.3718 1.83953 10.3132 2.48141 9.65756C3.11996 9.00631 4.15614 9.00631 4.79718 9.65756L9.94056 14.9603L19.2053 5.49041C19.8439 4.83653 20.8834 4.83653 21.5211 5.49041C22.1596 6.14254 22.1596 7.20203 21.5211 7.85765Z" fill="#596982"/>
                        </svg>
                      </div>
                      <div class="deny" @click="blockNameChange = false">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <g clip-path="url(#clip0)">
                        <path fill-rule="evenodd" clip-rule="evenodd" d="M19.7782 19.7784C19.0619 20.4946 17.9017 20.4946 17.1854 19.7784L12 14.5929L6.81455 19.7784C6.09831 20.4946 4.93807 20.4946 4.22182 19.7784C3.50558 19.0621 3.50559 17.9019 4.22183 17.1856L9.40728 12.0002L4.22183 6.81475C3.50559 6.09851 3.50559 4.93826 4.22183 4.22202C4.93807 3.50578 6.09831 3.50578 6.81455 4.22202L12 9.40747L17.1854 4.22202C17.901 3.50643 19.0619 3.50578 19.7782 4.22202C20.4944 4.93826 20.4938 6.09915 19.7782 6.81475L14.5927 12.0002L19.7782 17.1856C20.4944 17.9019 20.4944 19.0621 19.7782 19.7784Z" fill="#596982"/>
                        </g>
                        <defs>
                        <clipPath id="clip0">
                        <rect width="24" height="24" fill="white"/>
                        </clipPath>
                        </defs>
                        </svg>
                      </div>
                    </div>
                  </div>

                  <div v-else class="item__text" @click="blockNameChange = true">
                    {{ blockName }}
                    <span>
                      <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path fill-rule="evenodd" clip-rule="evenodd" d="M0.666992 12.2374V15.3337H3.45366L11.5203 6.28923L8.73366 3.19294L0.666992 12.2374ZM13.647 3.92628C13.9403 3.60035 13.9403 3.11146 13.647 2.78554L11.9603 0.911436C11.667 0.585511 11.227 0.585511 10.9337 0.911436L9.61366 2.3781L12.4003 5.47439L13.647 3.92628ZM7.26699 13.704L5.80033 15.3337H15.3337V13.704H7.26699Z" fill="#596982"/>
                      </svg>
                    </span>
                  </div>
                </div>

                <div class="item">
                  <div class="item__name">Категория объявлений</div>
                  <div class="item__buttons">
                    <div class="item__btn">Все</div>
                    <div class="item__btn active">Товары</div>
                    <div class="item__btn">Новости</div>
                  </div>
                </div>

                <div class="item">
                  <div class="item__name">
                    Рейтинг объявлений
                    <span>
                      <svg width="16" height="17" viewBox="0 0 16 17" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path fill-rule="evenodd" clip-rule="evenodd" d="M8.00033 15.8337C12.0581 15.8337 15.3337 12.5581 15.3337 8.50033C15.3337 4.44255 12.0581 1.16699 8.00033 1.16699C3.94255 1.16699 0.666992 4.44255 0.666992 8.50033C0.666992 12.5581 3.94255 15.8337 8.00033 15.8337ZM7.51144 3.70921C7.90255 3.70921 8.19588 4.00255 8.19588 4.39366C8.19588 4.78477 7.90255 5.0781 7.51144 5.0781C7.12033 5.0781 6.82699 4.78477 6.82699 4.39366C6.82699 4.05144 7.12033 3.70921 7.51144 3.70921ZM6.82699 6.44699C6.63144 6.44699 6.43588 6.25144 6.43588 6.05588C6.43588 5.86033 6.63144 5.66477 6.82699 5.66477H8.00033C8.19588 5.66477 8.39144 5.86033 8.39144 6.05588V11.8737H9.17366C9.36921 11.8737 9.56477 12.0692 9.56477 12.2648C9.56477 12.4603 9.36921 12.6559 9.17366 12.6559H6.82699C6.63144 12.6559 6.43588 12.4603 6.43588 12.2648C6.43588 12.0692 6.63144 11.8737 6.82699 11.8737H7.60921V6.44699H6.82699Z" fill="#596982"/>
                      </svg>

                      <q-tooltip
                        anchor="top left"
                        self="bottom left"
                        content-class="infopopup"
                        :offset="[170, 8]"
                      >
                        Вы можете указать объявления какого качества можно отображать на вашем сайте. Чем ниже рейтинг, тем большую доходность дает блок. <span>Выбор низкого рейтинга может дать доход на 10-20% выше, чем у. рейтинг 3!</span>
                      </q-tooltip>
                    </span>
                  </div>

                  <q-select
                    filled
                    v-model="filterSites"
                    input-debounce="0"
                    :label="rating[0]"
                    :options="rating"
                    style="height: 40px;"
                    dropdown-icon="keyboard_arrow_down"
                    popup-content-class="blocks-select"
                    behavior="menu"
                    menu-anchor="bottom left"
                    menu-self="top left"
                    :menu-offset="[1, -10]"
                  >
                  </q-select>
                </div>

                <div class="item">
                  <div class="item__name">
                    Форма блока
                  </div>
                  <div class="forms">
                    <div class="forms__header"></div>
                    <div class="forms__content active"></div>
                    <div class="forms__aside"></div>
                    <div class="forms__footer"></div>
                  </div>
                </div>

                <div class="item">
                  <div class="item__name">
                    Шаблоны
                    <span>
                      <svg width="16" height="17" viewBox="0 0 16 17" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path fill-rule="evenodd" clip-rule="evenodd" d="M8.00033 15.8337C12.0581 15.8337 15.3337 12.5581 15.3337 8.50033C15.3337 4.44255 12.0581 1.16699 8.00033 1.16699C3.94255 1.16699 0.666992 4.44255 0.666992 8.50033C0.666992 12.5581 3.94255 15.8337 8.00033 15.8337ZM7.51144 3.70921C7.90255 3.70921 8.19588 4.00255 8.19588 4.39366C8.19588 4.78477 7.90255 5.0781 7.51144 5.0781C7.12033 5.0781 6.82699 4.78477 6.82699 4.39366C6.82699 4.05144 7.12033 3.70921 7.51144 3.70921ZM6.82699 6.44699C6.63144 6.44699 6.43588 6.25144 6.43588 6.05588C6.43588 5.86033 6.63144 5.66477 6.82699 5.66477H8.00033C8.19588 5.66477 8.39144 5.86033 8.39144 6.05588V11.8737H9.17366C9.36921 11.8737 9.56477 12.0692 9.56477 12.2648C9.56477 12.4603 9.36921 12.6559 9.17366 12.6559H6.82699C6.63144 12.6559 6.43588 12.4603 6.43588 12.2648C6.43588 12.0692 6.63144 11.8737 6.82699 11.8737H7.60921V6.44699H6.82699Z" fill="#596982"/>
                      </svg>
                    </span>
                    <q-tooltip
                      anchor="top left"
                      self="bottom left"
                      content-class="infopopup"
                      :offset="[0, 8]"
                    >
                      <span>Шаблоны отсортированы в порядке доходности на основании общей статистики ads.bid (чем выше в списке, тем прибыльнее шаблон).</span> <br><br> Внимание! Показатели на отдельных сайтах могут отличаться.
                    </q-tooltip>
                  </div>
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
                  <div class="item__title">Повышение доходности</div>

                    <div class="checkbox">
                      <q-radio v-model="profitUp" val="autoload" label="Автоподгрузка" />
                      <span>
                        <svg width="16" height="17" viewBox="0 0 16 17" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" clip-rule="evenodd" d="M8.00033 15.8337C12.0581 15.8337 15.3337 12.5581 15.3337 8.50033C15.3337 4.44255 12.0581 1.16699 8.00033 1.16699C3.94255 1.16699 0.666992 4.44255 0.666992 8.50033C0.666992 12.5581 3.94255 15.8337 8.00033 15.8337ZM7.51144 3.70921C7.90255 3.70921 8.19588 4.00255 8.19588 4.39366C8.19588 4.78477 7.90255 5.0781 7.51144 5.0781C7.12033 5.0781 6.82699 4.78477 6.82699 4.39366C6.82699 4.05144 7.12033 3.70921 7.51144 3.70921ZM6.82699 6.44699C6.63144 6.44699 6.43588 6.25144 6.43588 6.05588C6.43588 5.86033 6.63144 5.66477 6.82699 5.66477H8.00033C8.19588 5.66477 8.39144 5.86033 8.39144 6.05588V11.8737H9.17366C9.36921 11.8737 9.56477 12.0692 9.56477 12.2648C9.56477 12.4603 9.36921 12.6559 9.17366 12.6559H6.82699C6.63144 12.6559 6.43588 12.4603 6.43588 12.2648C6.43588 12.0692 6.63144 11.8737 6.82699 11.8737H7.60921V6.44699H6.82699Z" fill="#596982"/>
                        </svg>
                        <q-tooltip
                          anchor="top left"
                          self="bottom left"
                          content-class="infopopup"
                          :offset="[150, 8]"
                        >
                          Рекомендуем ставить блок с включенной автоподгрузкой в конце статьи. <br>
                          При скролле бесконечно будут подгружаться тизеры.
                          Данный блок сможет повысить вашу доходность до 50%
                        </q-tooltip>
                      </span>
                    </div>
                    <div class="checkbox">
                      <q-radio v-model="profitUp" val="shape" label="Затемнение" />
                      <span>
                        <svg width="16" height="17" viewBox="0 0 16 17" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" clip-rule="evenodd" d="M8.00033 15.8337C12.0581 15.8337 15.3337 12.5581 15.3337 8.50033C15.3337 4.44255 12.0581 1.16699 8.00033 1.16699C3.94255 1.16699 0.666992 4.44255 0.666992 8.50033C0.666992 12.5581 3.94255 15.8337 8.00033 15.8337ZM7.51144 3.70921C7.90255 3.70921 8.19588 4.00255 8.19588 4.39366C8.19588 4.78477 7.90255 5.0781 7.51144 5.0781C7.12033 5.0781 6.82699 4.78477 6.82699 4.39366C6.82699 4.05144 7.12033 3.70921 7.51144 3.70921ZM6.82699 6.44699C6.63144 6.44699 6.43588 6.25144 6.43588 6.05588C6.43588 5.86033 6.63144 5.66477 6.82699 5.66477H8.00033C8.19588 5.66477 8.39144 5.86033 8.39144 6.05588V11.8737H9.17366C9.36921 11.8737 9.56477 12.0692 9.56477 12.2648C9.56477 12.4603 9.36921 12.6559 9.17366 12.6559H6.82699C6.63144 12.6559 6.43588 12.4603 6.43588 12.2648C6.43588 12.0692 6.63144 11.8737 6.82699 11.8737H7.60921V6.44699H6.82699Z" fill="#596982"/>
                        </svg>
                        <q-tooltip
                          anchor="top left"
                          self="bottom left"
                          content-class="infopopup"
                          :offset="[130, 8]"
                        >
                          Рекомендуем ставить блок с включенной автоподгрузкой в конце статьи. <br>
                          При скролле бесконечно будут подгружаться тизеры.
                          Данный блок сможет повысить вашу доходность до 50%
                        </q-tooltip>
                      </span>
                    </div>
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
            </q-tab-panel>

            <q-tab-panel name="wideSettings">
              <div class="card q-pa-none">
                <q-expansion-item
                  label="Настройки блока"
                  dropdown-icon="keyboard_arrow_down"
									group="group"
                >
                  <q-card>
                    <div class="item">
                      <div class="item__name">Отступ сверху</div>

                      <div class="item__ranges">
                        <div class="item__range">
                          <q-slider v-model="marginTop" :min="0" :max="10" label label-always />
                        </div>
                      </div>
                    </div>

                    <div class="item">
                      <div class="item__name">Отступ снизу</div>

                      <div class="item__ranges">
                        <div class="item__range">
                          <q-slider v-model="marginBottom" :min="0" :max="10" label label-always />
                        </div>
                      </div>
                    </div>

                    <div class="item">
                      <div class="item__name">Отступ слева</div>

                      <div class="item__ranges">
                        <div class="item__range">
                          <q-slider v-model="marginLeft" :min="0" :max="10" label label-always />
                        </div>
                      </div>
                    </div>

                    <div class="item">
                      <div class="item__name">Отступ справа</div>

                      <div class="item__ranges">
                        <div class="item__range">
                          <q-slider v-model="marginRight" :min="0" :max="10" label label-always />
                        </div>
                      </div>
                    </div>

                    <div class="item">
                      <div class="item__name">Цвет фона</div>

                      <q-input
                        filled
                        v-model="bgColor"
                        class="color-input"
                        anchor="top left"
                        self="bottom left"
                      >
                        <template v-slot:append>
                          <q-icon class="cursor-pointer" :style="{background: bgColor}">
                            <q-popup-proxy>
                              <q-color v-model="bgColor" no-header no-footer />
                            </q-popup-proxy>
                          </q-icon>
                        </template>
                      </q-input>
                    </div>

                    <div class="item">
                      <div class="item__name">Толщина рамки</div>

                      <div class="item__ranges">
                        <div class="item__range">
                          <q-slider v-model="borderWidth" :min="0" :max="10" label label-always />
                        </div>
                      </div>
                    </div>

                    <div class="item">
                      <div class="item__name">
                        Стиль рамки
                      </div>

                      <q-select
                        class="border-select"
                        filled
                        v-model="borderBlocks"
                        input-debounce="0"
                        :label="borderStyle[0]"
                        :options="borderStyle"
                        style="height: 40px;"
                        dropdown-icon="keyboard_arrow_down"
                        popup-content-class="border-select"
                        behavior="menu"
                        menu-anchor="bottom left"
                        menu-self="top left"
                        :menu-offset="[1, -10]"
                      >
                      </q-select>
                    </div>

                     <div class="item">
                      <div class="item__name">Цвет рамки</div>

                      <q-input
                        filled
                        v-model="borderColor"
                        class="color-input"
                        anchor="top left"
                        self="bottom left"
                      >
                        <template v-slot:append>
                          <q-icon class="cursor-pointer" :style="{background: borderColor}">
                            <q-popup-proxy>
                              <q-color v-model="borderColor" no-header no-footer />
                            </q-popup-proxy>
                          </q-icon>
                        </template>
                      </q-input>
                    </div>
                  </q-card>
                </q-expansion-item>

                <q-expansion-item
                  label="Настройки тизера"
                  dropdown-icon="keyboard_arrow_down"
									group="group"
                >
                  <q-card>
                    <p>Настройки тизера</p>
                  </q-card>
                </q-expansion-item>

                <q-expansion-item
                  label="Настройки изображения"
                  dropdown-icon="keyboard_arrow_down"
									group="group"
                >
                  <q-card>
                    <p>Настройки изображения</p>
                  </q-card>
                </q-expansion-item>

                <q-expansion-item
                  label="Настройки текста"
                  dropdown-icon="keyboard_arrow_down"
									group="group"
                >
                  <q-card>
                    <p>Настройки текста</p>
                  </q-card>
                </q-expansion-item>

                <q-expansion-item
                  label='Настройки кнопки "Читать далее"'
                  dropdown-icon="keyboard_arrow_down"
									group="group"
                >
                  <q-card>
                    <p>Настройки кнопки "Читать далее"</p>
                  </q-card>
                </q-expansion-item>
              </div>
            </q-tab-panel>
          </q-tab-panels>

          <div class="card blocks">
          <div class="blocks__head">
            <div class="blocks__fullscreen">
              <svg width="22" height="22" viewBox="0 0 22 22" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path fill-rule="evenodd" clip-rule="evenodd" d="M22 0V8.24725L19.2514 5.49725L15.1277 9.62225L12.3777 6.875L16.5028 2.74175L13.7527 0H22V0ZM6.87775 12.3723L2.75137 16.4972L0 13.7473V22H8.25275L5.50275 19.2555L9.62775 15.125L6.87775 12.3723ZM15.125 12.3777L12.3777 15.1277L16.5028 19.2528L13.7527 22H22V13.7527L19.2582 16.5028L15.125 12.3777ZM8.25275 0H0V8.25275L2.7445 5.50275L6.875 9.62775L9.62775 6.87775L5.50275 2.75275L8.25275 0Z" fill="#596982"/>
              </svg>
            </div>
            <q-btn class="btn btn-red" :ripple="false" label="Сбросить настройки" unelevated no-caps />
          </div>

          <div class="blocks__container">
            <div class="box__row">
              <div class="box__column">
                <a href="#" class="box__item item-box">
                  <div class="item-box__image">
                    <img src="https://6jfvnf69jx.ru/33-5f6473df554e45f6473df555b7.jpg" alt="">
                  </div>
                  <div class="item-box__text">
                    <div class="item-box__descr">
                      Большой живот не от еды! Он уйдёт за 5-10 дней, натощак пейте обычный крепкий...
                    </div>
                    <div class="item-box__bottom">
                      <div class="item-box__date"><span>3</span> ч. назад</div>
                      <div class="item-box__menu"></div>
                    </div>
                  </div>
                </a>
              </div>
              <div class="box__column">
                <a href="#" class="box__item item-box">
                  <div class="item-box__image">
                    <img src="https://6jfvnf69jx.ru/33-5f6473df554e45f6473df555b7.jpg" alt="">
                  </div>
                  <div class="item-box__text">
                    <div class="item-box__descr">
                      Большой живот не от еды! Он уйдёт за 5-10 дней, натощак пейте обычный крепкий...
                    </div>
                    <div class="item-box__bottom">
                      <div class="item-box__date"><span>3</span> ч. назад</div>
                      <div class="item-box__menu"></div>
                    </div>
                  </div>
                </a>
              </div>
              <div class="box__column">
                <a href="#" class="box__item item-box">
                  <div class="item-box__image">
                    <img src="https://6jfvnf69jx.ru/33-5f6473df554e45f6473df555b7.jpg" alt="">
                  </div>
                  <div class="item-box__text">
                    <div class="item-box__descr">
                      Большой живот не от еды! Он уйдёт за 5-10 дней, натощак пейте обычный крепкий...
                    </div>
                    <div class="item-box__bottom">
                      <div class="item-box__date"><span>3</span> ч. назад</div>
                      <div class="item-box__menu"></div>
                    </div>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
      </q-card>


  </q-page>
</template>

<script>
export default {
  data() {
    return {
      tab: "fastSettings",
      filterSites: null,
      borderBlocks: null,
      rating: [
        "Рейтинг 1 (Объявления вызывающего характера, в том числе с рекламой тематикой: мужское/женское здоровье)","Рейтинг 2 (Объявления умеренного содержания, но допускается реклама мужского/женского здоровья)",
        "Рейтинг 3 (Объявления умеренного содержания)"
      ],
      borderStyle: ['Сплошная', 'Пунктирная', 'Точки'],
      rows: 6,
      columns: 6,
      profitUp: 'autoload',
      blockNameChange: false,
      blockName: '31.03.2021_11:12:44',
      marginTop: 6,
      marginBottom: 6,
      marginLeft: 6,
      marginRight: 6,
      bgColor: 'White',
      borderColor: 'White',
      borderWidth: 6
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
      margin: 0px 0px 39px 0px;

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
      margin: 0px 0px 30px 0px;
      padding: 0px 0px 0px 0px;
      align-items: center;

      .device {
        display: flex;
        align-items: center;
        margin: 3px 0px 0px auto;

        .pc {
          margin: 0px 31px 0px 0px;
        }

        .mob {
          margin: 0px 6px 0px 0px;
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
      margin: 0px 0 0 0;
      min-height: 0;
      padding: 0px;

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
          margin: -3px 0px 24px 0px;

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
            margin: 9px 16px 7px 16px;
            overflow: hidden;
            font-size: 16px;
            line-height: 20px;
            letter-spacing: -0.1px;

            span {
              position: absolute;
              top: 9px;
              max-height: 20px;
              overflow: hidden;
            }

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

        .q-expansion-item {
          & + .q-expansion-item {
            border-top: 1px solid #DBDFE4;
          }

          .q-focus-helper {
            display: none;
          }

          .q-item {
            padding: 27px 40px;
            margin: 0;
            min-height: 22px;

            &__label {
              font-weight: 500;
              font-size: 18px;
              line-height: 22px;
              color: #12284C;
            }
          }

          .q-icon {
            color: #A0A9B7;
            font-size: 34px;
            margin: 0px -5px 0px 0px;
          }

          &__content {
            max-width: 496px;
            padding: 0 40px;

            .q-card {
              .item {
                margin: 1px 0px 24px 0px;

                &__changename {
                  .q-field--labeled .q-field__native{
                    padding-top: 0px;
                    padding-bottom: 0;
                  }

                  .q-field--focused {
                    border-color: #12284C;
                  }

                  .actions {
                    margin: -12px 0px 0px 0px;
                    display: flex;
                    justify-content: flex-end;

                    .accept {
                      margin: 0px 24px 0px 0px;
                      cursor: pointer;
                    }

                    .deny {
                      cursor: pointer;
                    }
                  }
                }

                &__name {
                  display: flex;
                  font-weight: 500;
                  font-size: 14px;
                  line-height: 17px;
                  color: #A0A9B7;
                  margin: 0px 0px 15px 0px;

                  span {
                    display: inline-block;
                    margin: 0px 0px 0px 13px;
                    position: relative;
                    top: 0px;
                    cursor: pointer;
                  }
                }

                &__text, &__btn {
                  font-size: 16px;
                  line-height: 20px;
                  color: #12284C;
                }

                &__text {
                  span {
                    display: inline-block;
                    margin: 0px 0px 0px 8px;
                    position: relative;
                    top: 2px;
                    cursor: pointer;
                  }
                }

                &__title {
                  font-size: 16px;
                  line-height: 20px;
                  color: #273B5B;
                  margin: 0px 0px 14px 0px;
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

                  &.active{
                    border: 1px solid #4690FF;
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
                  margin: 30px 0px 0
                }

                &__range {
                  padding: 0px;

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

                .checkbox {
                  & + .checkbox {
                    margin: 11px 0px 0px 0px;
                  }

                  span {
                    position: relative;
                    top: 3px;
                    cursor: pointer;
                  }
                }

                .q-radio {
                  height: 15px;
                  margin: 0px 17px 0px 0px;

                  &__inner {
                    font-size: 16px;
                    width: 15px;
                    min-width: 15px;
                    height: 15px;
                    outline: 0;
                    border-radius: 50%;
                    color: #596982;
                    margin: -2px 8px 0px 0px;

                    &::before {
                      content:'';
                      display: none;
                    }

                    &::after {
                      content:'';
                      position: absolute;
                      width: 16px;
                      height: 16px;
                      top: 0px;
                      left: 0px;
                      background-color: #fff;
                      z-index: 10 !important;
                      background: url('../assets/checkbox-default-16.svg') 0 0/ contain no-repeat;
                    }

                    &--truthy {
                      .q-radio__bg {
                        color: #fff;
                        border: 2px solid transparent !important;
                        position: relative;
                        border-radius: 2px;

                        svg {
                          z-index: 1;
                        }
                      }

                      &::after {
                        content:'';
                        position: absolute;
                        width: 16px;
                        height: 16px;
                        top: 0px;
                        left: 0px;
                        background-color: #fff;
                        z-index: 10 !important;
                        background: url('../assets/checkbox-default-16-active.svg') 0 0/ contain no-repeat;
                      }
                    }

                    .q-radio__svg {
                      color: #12284C;

                      path {
                        fill: #fff;
                      }

                      &.absolute-full {
                        top: -2px;
                        transform: translate(1px, 0);
                      }
                    }

                    .q-radio__bg {
                      color: #fff;
                      position: relative;
                      border-radius: 2px;

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

                  &__bg {
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                  }

                  &__label {
                    font-size: 14px;
                  }
                }

                .color-input {
                  i {
                    margin: -18px 8px 0px 0px;
                    width: 24px;
                    height: 24px;
                    border: 1px solid #A0A9B7;
                    border-radius: 4px;
                  }
                }

                .border-select {
                  i {
                    color: #4690FF;
                    margin: -16px 8px 0 0;
                    font-size: 25px;
                  }
                }

                &:last-child {
                  margin: 0px 0px 32px 0px;
                }
              }
            }
          }
        }
      }

      &-panels {
        flex: 0 1 460px;
        margin: 0px 40px 0px 0px;

        .scroll {
          overflow: visible;
        }
      }

      &__label {
        color: #596982;
        font-size: 18px;
        line-height: 25px;
        letter-spacing: -0.1px;
        margin: 0px 0px 0px 0px;

        &:hover{
          color: #12284C !important;
        }

        @media (max-width:1360px){
          font-size: 16px !important;
          line-height: 20px;
        }
      }

      & + .q-tab {
        margin: 0px 0px 0px 24px;

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
          top: -2px;
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
        margin: -4px 0px 0px 0px;
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

        &.q-pa-none {
          padding: 0 !important;
        }
      }

      .settings {
        .item {
          margin: 1px 0px 24px 0px;

          &__changename {
            .q-field--labeled .q-field__native{
              padding-top: 0px;
              padding-bottom: 0;
            }

            .q-field--focused {
              border-color: #12284C;
            }

            .actions {
              margin: -12px 0px 0px 0px;
              display: flex;
              justify-content: flex-end;

              .accept {
                margin: 0px 24px 0px 0px;
                cursor: pointer;
              }

              .deny {
                cursor: pointer;
              }
            }
          }

          &__name {
            display: flex;
            font-weight: 500;
            font-size: 14px;
            line-height: 17px;
            color: #A0A9B7;
            margin: 0px 0px 15px 0px;

            span {
              display: inline-block;
              margin: 0px 0px 0px 13px;
              position: relative;
              top: 0px;
              cursor: pointer;
            }
          }

          &__text, &__btn {
            font-size: 16px;
            line-height: 20px;
            color: #12284C;
          }

          &__text {
            span {
              display: inline-block;
              margin: 0px 0px 0px 8px;
              position: relative;
              top: 2px;
              cursor: pointer;
            }
          }

          &__title {
            font-size: 16px;
            line-height: 20px;
            color: #273B5B;
            margin: 0px 0px 14px 0px;
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

            &.active{
              border: 1px solid #4690FF;
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

          .checkbox {
            & + .checkbox {
              margin: 11px 0px 0px 0px;
            }

            span {
              position: relative;
              top: 3px;
              cursor: pointer;
            }
          }

          .q-radio {
            height: 15px;
            margin: 0px 17px 0px 0px;

            &__inner {
              font-size: 16px;
              width: 15px;
              min-width: 15px;
              height: 15px;
              outline: 0;
              border-radius: 50%;
              color: #596982;
              margin: -2px 8px 0px 0px;

              &::before {
                content:'';
                display: none;
              }

              &::after {
                content:'';
                position: absolute;
                width: 16px;
                height: 16px;
                top: 0px;
                left: 0px;
                background-color: #fff;
                z-index: 10 !important;
                background: url('../assets/checkbox-default-16.svg') 0 0/ contain no-repeat;
              }

              &--truthy {
                .q-radio__bg {
                  color: #fff;
                  border: 2px solid transparent !important;
                  position: relative;
                  border-radius: 2px;

                  svg {
                    z-index: 1;
                  }
                }

                &::after {
                  content:'';
                  position: absolute;
                  width: 16px;
                  height: 16px;
                  top: 0px;
                  left: 0px;
                  background-color: #fff;
                  z-index: 10 !important;
                  background: url('../assets/checkbox-default-16-active.svg') 0 0/ contain no-repeat;
                }
              }

              .q-radio__svg {
                color: #12284C;

                path {
                  fill: #fff;
                }

                &.absolute-full {
                  top: -2px;
                  transform: translate(1px, 0);
                }
              }

              .q-radio__bg {
                color: #fff;
                position: relative;
                border-radius: 2px;

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

            &__bg {
              top: 0;
              left: 0;
              width: 100%;
              height: 100%;
            }

            &__label {
              font-size: 14px;
            }
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
            padding: 0px;
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
              cursor: pointer;
              border: 1px solid #f0f5fd;
              background-color: #f0f5fd;
            }
          }
        }
      }

      .blocks {
        flex: 1 1 auto;
        max-width: calc(100% - 500px);

        &__head {
          display: flex;
          justify-content: space-between;
          align-items: center;
          margin: 0px 0px 32px 0px;
        }

        &__fullscreen {
          cursor: pointer;
          margin: 4px 0px 0px 0px;
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
            z-index: 1;

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

  .q-menu {
    &.blocks-select, &.border-select {
      width: 380px;

      .q-item {
        &:hover{
          background: #f3f4f6;
        }

        &__label {
          color: #12284C;
        }

        .q-focus-helper {
          display: none;
        }
      }
    }
  }

  /**
		ОБЪЯВЛЕНИЯ С ДАТОЙ ПУБЛИКАЦИИ===========================================================================================================================================================
		**/

		.box__row {
			font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
			display: -webkit-box;
			display: -ms-flexbox;
			display: flex;
			-ms-flex-wrap: wrap;
			flex-wrap: wrap;
			margin: 0 -4px;
		}

		.box__column {
			padding: 0px 4px;
			display: -webkit-box;
			display: -ms-flexbox;
			display: flex;
			margin: 0px 0px 25px 0px;
			-webkit-box-flex: 0;
					-ms-flex: 0 1 33.333%;
							flex: 0 1 33.333%;
			margin: 0 auto;
		}

		.item-box {
			text-decoration: none;
			margin: 0 auto;
			max-width: 492px;
			display: -webkit-box;
			display: -ms-flexbox;
			display: flex;
			-webkit-box-orient: vertical;
			-webkit-box-direction: normal;
			-ms-flex-direction: column;
			flex-direction: column;
			border-radius: 4px;
			overflow: hidden;
			-webkit-box-shadow: 0 4px 15px rgba(0, 0, 0, 0.07), 0 5px 15px rgba(0, 0, 0, 0.07);
			box-shadow: 0 4px 15px rgba(0, 0, 0, 0.07), 0 5px 15px rgba(0, 0, 0, 0.07);
		}

		.item-box__image {
			position: relative;
			padding: 0px 0px 66.668% 0px;
		}

		@media (max-width: 1280px) {
			.item-box__image {
				padding: 0;
				height: 300px;
			}
		}

		.item-box__image img {
			position: absolute;
			width: 100%;
			height: 100%;
			top: 0;
			left: 0;
			-o-object-fit: cover;
			object-fit: cover;
		}

		.item-box__text {
			padding: 15px;
			text-align: left;
			display: -webkit-box;
			display: -ms-flexbox;
			display: flex;
			-webkit-box-orient: vertical;
			-webkit-box-direction: normal;
			-ms-flex-direction: column;
			flex-direction: column;
			color: #202125;
		}

		@media (max-width: 425px) {
			.item-box__text {
				padding: 5px;
			}
		}

		.item-box__descr {
			font-size: 2vw;
			line-height: 1.2;
			font-weight: 400;
			-webkit-box-flex: 1;
			-ms-flex: 1 1 auto;
			flex: 1 1 auto;
			margin: 0px 0px 15px 0px;
			overflow: hidden;
			-o-text-overflow: ellipsis;
			text-overflow: ellipsis;
			display: -moz-box;
			display: -webkit-box;
			-webkit-line-clamp: 5;
			-webkit-box-orient: vertical;
			line-clamp: 5;
			box-orient: vertical;
		}

		@media (max-width: 1024px) {
			.item-box__descr {
				font-size: 3vw;
			}
		}

		@media (max-width: 768px) {
			.item-box__descr {
				font-size: 20px;
			}
		}

		@media (max-width: 320px) {
			.item-box__descr {
				font-size: 18px;
			}
		}

		.item-box__bottom {
			display: -webkit-box;
			display: -ms-flexbox;
			display: flex;
			-webkit-box-pack: justify;
			-ms-flex-pack: justify;
			justify-content: space-between;
			-webkit-box-align: center;
			-ms-flex-align: center;
			align-items: center;
		}

		.item-box__menu {
			width: 22px;
			height: 22px;
			background: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAAWCAMAAADzapwJAAAAdVBMVEVHcEyIi5BscXO/wMSQlJfJyMzDw8bOz9La3uGXmp6GjY+/wMJtbnOIiYyMjZO1tLd9foLg5ul8gofY2duytLrX2t20tLaUlpnCw8VYXWFjZ2xmam9ydXlvcXRmZ2p2dnlfZm15e39QVlpgY2dbYmV8gINscnVal1D1AAAAGXRSTlMA1/NYuC4sKhq0w1jzwrpy4C3nI3Qkardue3dt2QAAAFNJREFUGBmtwcUBgDAQBMBFk+AOh3v/JVLAPsMM/hUnqQZR2ygGJFwmycCavSpha3icFiR4b/FBwvk6e7DucGrYytdCgQTLJD6ImkcxYJ4bafzqA/sYA+fS0lmUAAAAAElFTkSuQmCC') center/contain no-repeat;
		}

		// /**
		// ОБЪЯВЛЕНИЯ С ДАТОЙ ПУБЛИКАЦИИ===========================================================================================================================================================
		// **/
</style>
