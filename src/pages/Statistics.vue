<template>
  <q-page :class="['statistics-page', { lock: lockPage }]">
    <div class="title-mob">Статистика</div>

    <div class="row filters">
      <q-btn-dropdown
        class="datepicker"
        label="4.01.21 - 10.01.21"
        :ripple="false"
        content-class="datepicker-popup"
        menu-anchor="bottom left"
        menu-self="top left"
        @input="lockPage = !lockPage"
        v-model="datepicker"
      >
        <div class="datepicker-menu">
          <div class="datepicker-nav">
            <div class="datepicker-reset" @click="dateOne = null, dateTwo = null">Сбросить</div>
            <div class="datepicker-title">Период</div>
            <div class="datepicker-close active" @click="datepicker = false">
              <svg
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <g clip-path="url(#clip0)">
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M19.7782 19.7784C19.0619 20.4946 17.9017 20.4946 17.1854 19.7784L12 14.5929L6.81455 19.7784C6.09831 20.4946 4.93807 20.4946 4.22182 19.7784C3.50558 19.0621 3.50559 17.9019 4.22183 17.1856L9.40728 12.0002L4.22183 6.81475C3.50559 6.09851 3.50559 4.93826 4.22183 4.22202C4.93807 3.50578 6.09831 3.50578 6.81455 4.22202L12 9.40747L17.1854 4.22202C17.901 3.50643 19.0619 3.50578 19.7782 4.22202C20.4944 4.93826 20.4938 6.09915 19.7782 6.81475L14.5927 12.0002L19.7782 17.1856C20.4944 17.9019 20.4944 19.0621 19.7782 19.7784Z"
                    fill="#596982"
                  />
                </g>
                <defs>
                  <clipPath id="clip0">
                    <rect width="24" height="24" fill="white" />
                  </clipPath>
                </defs>
              </svg>
            </div>
          </div>
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

          <q-date v-model="dateTwo" minimal range />

          <div
            class="datepicker-btn"
            :ripple="false"
            @click="datepicker = false"
          >
            Отменить
          </div>

          <div class="datepicker-btn-two" :ripple="false" @click="datepicker = false">
            <span class="active">Готово</span>
          </div>
        </div>
      </q-btn-dropdown>

      <q-select
        filled
        v-model="group"
        multiple
        :options="groupOptions"
        label="Группировать по:"
        style="width: 213px; height: 40px"
        dropdown-icon="keyboard_arrow_down"
        popup-content-class="group-popup"
        behavior="menu"
        @popup-show="lockPage = !lockPage"
        @popup-hide="lockPage = !lockPage"
      >
        <template v-slot:option="groupOptions">
          <div class="group-menu">
            <div class="group-nav">
              <div class="group-reset" @click="group = null">Сбросить</div>
              <div class="group-title">Группировать по:</div>
              <div class="group-close active">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g clip-path="url(#clip0)">
                    <path
                      fill-rule="evenodd"
                      clip-rule="evenodd"
                      d="M19.7782 19.7784C19.0619 20.4946 17.9017 20.4946 17.1854 19.7784L12 14.5929L6.81455 19.7784C6.09831 20.4946 4.93807 20.4946 4.22182 19.7784C3.50558 19.0621 3.50559 17.9019 4.22183 17.1856L9.40728 12.0002L4.22183 6.81475C3.50559 6.09851 3.50559 4.93826 4.22183 4.22202C4.93807 3.50578 6.09831 3.50578 6.81455 4.22202L12 9.40747L17.1854 4.22202C17.901 3.50643 19.0619 3.50578 19.7782 4.22202C20.4944 4.93826 20.4938 6.09915 19.7782 6.81475L14.5927 12.0002L19.7782 17.1856C20.4944 17.9019 20.4944 19.0621 19.7782 19.7784Z"
                      fill="#596982"
                    />
                  </g>
                  <defs>
                    <clipPath id="clip0">
                      <rect width="24" height="24" fill="white" />
                    </clipPath>
                  </defs>
                </svg>
              </div>
            </div>
          </div>

          <q-item
            v-bind="groupOptions.itemProps"
            v-on="groupOptions.itemEvents"
          >
            <div v-html="groupOptions.opt"></div>
          </q-item>

          <div class="group-btn" :ripple="false" @click="group = null">
            <span class="active">Готово</span>
          </div>
        </template>
      </q-select>

      <div class="filter__wrp">
        <span
          class="filter-counter"
          :class="{ active: filterOne || filterTwo !== null }"
          >1</span
        >
        <q-btn-dropdown
          class="filter"
          :class="{ active: filterOne || filterTwo !== null }"
          label="Фильтры"
          :ripple="false"
          no-caps
          menu-anchor="bottom left"
          menu-self="top left"
          content-class="filter-popup"
          @input="lockPage = !lockPage"
          v-model="filter"
        >
          <div class="filter-menu">
            <div class="filter-nav">
              <div class="filter-reset" @click.stop="(filterOne = null), (filterTwo = null)">Сбросить</div>
              <div class="filter-title">Фильтры</div>
              <div class="filter-close active" @click="filter = false">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g clip-path="url(#clip0)">
                    <path
                      fill-rule="evenodd"
                      clip-rule="evenodd"
                      d="M19.7782 19.7784C19.0619 20.4946 17.9017 20.4946 17.1854 19.7784L12 14.5929L6.81455 19.7784C6.09831 20.4946 4.93807 20.4946 4.22182 19.7784C3.50558 19.0621 3.50559 17.9019 4.22183 17.1856L9.40728 12.0002L4.22183 6.81475C3.50559 6.09851 3.50559 4.93826 4.22183 4.22202C4.93807 3.50578 6.09831 3.50578 6.81455 4.22202L12 9.40747L17.1854 4.22202C17.901 3.50643 19.0619 3.50578 19.7782 4.22202C20.4944 4.93826 20.4938 6.09915 19.7782 6.81475L14.5927 12.0002L19.7782 17.1856C20.4944 17.9019 20.4944 19.0621 19.7782 19.7784Z"
                      fill="#596982"
                    />
                  </g>
                  <defs>
                    <clipPath id="clip0">
                      <rect width="24" height="24" fill="white" />
                    </clipPath>
                  </defs>
                </svg>
              </div>
            </div>

            <div class="filter-menu__row">
              <q-select
                filled
                v-model="filterOne"
                input-debounce="0"
                label="Выберите фильтр"
                :options="optionsOne"
                style="width: 217px; height: 40px"
                dropdown-icon="keyboard_arrow_down"
                popup-content-class="filterOne"
                behavior="menu"
              >
              </q-select>

              <q-select
                filled
                v-model="filterTwo"
                use-input
                input-debounce="0"
                label="Выберите или введите значение"
                :options="optionsTwo"
                style="width: 401px; height: 40px"
                dropdown-icon="keyboard_arrow_down"
                use-chips
                multiple
                popup-content-class="filterTwo"
                behavior="menu"
                @new-value="createValue"
              >
              </q-select>

              <div class="filter-menu__close" :active="'После добавления второго filter-menu__row'">
                <svg
                  width="16"
                  height="16"
                  viewBox="0 0 16 16"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M13.1854 13.1853C12.708 13.6627 11.9345 13.6627 11.457 13.1853L8 9.72829L4.54303 13.1853C4.06554 13.6627 3.29204 13.6627 2.81455 13.1853C2.33706 12.7078 2.33706 11.9343 2.81455 11.4568L6.27152 7.9998L2.81455 4.54284C2.33706 4.06534 2.33706 3.29185 2.81455 2.81436C3.29204 2.33686 4.06554 2.33686 4.54303 2.81436L8 6.27132L11.457 2.81436C11.934 2.33729 12.708 2.33686 13.1854 2.81435C13.6629 3.29185 13.6625 4.06578 13.1854 4.54284L9.72848 7.9998L13.1854 11.4568C13.6629 11.9343 13.6629 12.7078 13.1854 13.1853Z"
                    fill="#B8BFC9"
                  />
                </svg>
              </div>
              <q-btn
                class="btn btn-red btn-del active"
                label="Удалить фильтр"
                unelevated
                no-caps
                :ripple="false"
              />
            </div>

            <div class="filter-menu__buttons">
              <q-btn
                class="btn btn-white"
                label="Добавить фильтр"
                unelevated
                no-caps
                v-ripple:blue-14.center
              />
              <q-btn
                class="btn btn-red btn-reset"
                @click.stop="(filterOne = null), (filterTwo = null)"
                label="Сбросить все"
                unelevated
                no-caps
                :ripple="false"
              />
              <q-btn
                class="btn btn-blue active"
                label="Готово"
                :ripple="false"
                unelevated
                no-caps
                @click="filter = false"
              />
              <q-btn
                class="btn btn-grey"
                :ripple="false"
                label="Отменить"
                unelevated
                no-caps
                @click="filter = false"
              />
            </div>
          </div>
        </q-btn-dropdown>
      </div>

      <q-btn class="btn" :ripple="false" label="Показать" unelevated no-caps />

      <q-toggle
        class="chart-toggle"
        v-model="chartToggle"
        label="График"
        left-label
      />

      <div class="cvs-icon">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <g clip-path="url(#clip0)">
        <path d="M21.1463 21.0176C21.1463 22.0137 20.3388 22.8211 19.3428 22.8211H4.91482C3.91878 22.8211 3.11133 22.0137 3.11133 21.0176V2.98269C3.11133 1.98665 3.91878 1.1792 4.91482 1.1792H9.95179H14.9888C15.4671 1.1792 15.9258 1.36921 16.264 1.70743L18.441 3.88444L20.618 6.06145C20.9563 6.39967 21.1463 6.85839 21.1463 7.33671V15.1047" stroke="#596982"/>
        <path d="M17.5914 12.0016H2.35189C1.67558 11.9991 0.999268 10.7454 0.999268 10.6465V18.8108C0.999268 19.4998 1.70884 19.7869 2.06362 19.8443H17.5914V12.0016Z" fill="#596982"/>
        <path d="M0.999268 10.6475C0.999268 9.90051 1.60486 9.29492 2.35189 9.29492H2.64929V10.6475V12.0002H2.35189C1.60486 12.0002 0.999268 11.3946 0.999268 10.6475Z" fill="#596982"/>
        <path d="M4.85631 18.4925C4.33193 18.4925 3.85702 18.3773 3.43158 18.1468C3.01109 17.9114 2.67964 17.5883 2.43724 17.1775C2.19978 16.7667 2.08105 16.3033 2.08105 15.7873C2.08105 15.2713 2.20226 14.8079 2.44466 14.3971C2.68706 13.9863 3.01851 13.6657 3.439 13.4352C3.86444 13.1998 4.33935 13.082 4.86373 13.082C5.28917 13.082 5.67751 13.1572 6.02874 13.3075C6.37998 13.4578 6.6768 13.6757 6.9192 13.9612L6.29588 14.5549C5.91991 14.1441 5.45737 13.9387 4.90825 13.9387C4.55207 13.9387 4.23299 14.0188 3.95101 14.1792C3.66903 14.3345 3.44889 14.5524 3.29059 14.8329C3.13229 15.1135 3.05314 15.4316 3.05314 15.7873C3.05314 16.143 3.13229 16.4611 3.29059 16.7416C3.44889 17.0222 3.66903 17.2426 3.95101 17.4029C4.23299 17.5582 4.55207 17.6359 4.90825 17.6359C5.45737 17.6359 5.91991 17.428 6.29588 17.0121L6.9192 17.6133C6.6768 17.8989 6.37751 18.1168 6.02132 18.2671C5.67009 18.4174 5.28175 18.4925 4.85631 18.4925Z" fill="white"/>
        <path d="M9.42477 18.4925C9.02406 18.4925 8.63572 18.4349 8.25975 18.3197C7.88873 18.2045 7.59438 18.0517 7.37672 17.8613L7.71064 17.1023C7.92336 17.2727 8.18307 17.4129 8.48979 17.5231C8.80145 17.6283 9.11311 17.6809 9.42477 17.6809C9.81063 17.6809 10.0976 17.6183 10.2855 17.4931C10.4785 17.3678 10.5749 17.2025 10.5749 16.9971C10.5749 16.8468 10.5205 16.7241 10.4117 16.6289C10.3078 16.5287 10.1742 16.4511 10.011 16.396C9.84773 16.3408 9.62512 16.2782 9.34314 16.2081C8.94738 16.1129 8.62583 16.0177 8.37848 15.9225C8.13608 15.8274 7.92583 15.6796 7.74774 15.4792C7.5746 15.2738 7.48802 14.9982 7.48802 14.6526C7.48802 14.362 7.5647 14.099 7.71806 13.8635C7.87636 13.6231 8.11134 13.4327 8.423 13.2924C8.73961 13.1522 9.12547 13.082 9.5806 13.082C9.8972 13.082 10.2089 13.1221 10.5156 13.2023C10.8223 13.2824 11.087 13.3976 11.3096 13.5479L11.0053 14.3069C10.7778 14.1716 10.5403 14.0689 10.293 13.9988C10.0456 13.9287 9.80568 13.8936 9.57318 13.8936C9.19226 13.8936 8.90781 13.9587 8.71982 14.089C8.53678 14.2192 8.44526 14.3921 8.44526 14.6075C8.44526 14.7578 8.49721 14.8805 8.60109 14.9757C8.70993 15.0709 8.84597 15.146 9.00922 15.2011C9.17247 15.2562 9.39508 15.3189 9.67706 15.389C10.0629 15.4792 10.3795 15.5744 10.6269 15.6746C10.8742 15.7697 11.0845 15.9175 11.2576 16.1179C11.4357 16.3183 11.5248 16.5888 11.5248 16.9295C11.5248 17.22 11.4456 17.4831 11.2873 17.7185C11.1339 17.954 10.899 18.1418 10.5824 18.2821C10.2658 18.4224 9.87989 18.4925 9.42477 18.4925Z" fill="white"/>
        <path d="M17.2304 13.1572L14.9672 18.4174H14.0173L11.7467 13.1572H12.793L14.5219 17.215L16.2657 13.1572H17.2304Z" fill="white"/>
        <path d="M18.4415 3.88444L16.2645 1.70743C15.9262 1.36921 15.4675 1.1792 14.9892 1.1792H14.8345V5.68793C14.8345 6.68398 15.6419 7.49143 16.638 7.49143H21.1467V7.33671C21.1467 6.8584 20.9567 6.39967 20.6185 6.06145L18.4415 3.88444Z" fill="#596982"/>
        <g filter="url(#filter0_d)">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M21.6086 18.0284V16.1733H20.6811V18.0284H19.2898L21.1448 19.8834L22.9998 18.0284H21.6086Z" fill="#596982"/>
        </g>
        </g>
        <defs>
        <filter id="filter0_d" x="-5.71021" y="-8.82666" width="53.71" height="53.71" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
        <feFlood flood-opacity="0" result="BackgroundImageFix"/>
        <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"/>
        <feOffset/>
        <feGaussianBlur stdDeviation="12.5"/>
        <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.08 0"/>
        <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow"/>
        <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow" result="shape"/>
        </filter>
        <clipPath id="clip0">
        <rect width="24" height="24" fill="white"/>
        </clipPath>
        </defs>
        </svg>
      </div>
    </div>

    <q-card v-if="chartToggle">
      <q-tabs v-model="tabCharts" align="left">
        <q-tab :ripple="false" name="profit" label="Доход" no-caps></q-tab>
        <q-tab :ripple="false" name="shows" label="Показы" no-caps></q-tab>
        <q-tab :ripple="false" name="clicks" label="Клики" no-caps></q-tab>
        <q-tab
          :ripple="false"
          name="uniqclicks"
          label="Ун. клики"
          no-caps
        ></q-tab>
        <q-tab :ripple="false" name="ctr" label="CTR" no-caps></q-tab>
        <q-tab :ripple="false" name="cpm" label="CPM" no-caps></q-tab>
      </q-tabs>

      <q-tab-panels v-model="tabCharts" animated>
        <q-tab-panel name="profit">
          <div class="chart">
            <img class="graphic-big" src="../assets/graphic-big.jpg" alt="" />
            <img
              class="graphic-desktop"
              src="../assets/graphic-desktop.jpg"
              alt=""
            />
            <img class="graphic-mob" src="../assets/chart_mob.jpg" alt="" />
          </div>
        </q-tab-panel>
        <q-tab-panel name="shows">
          <div class="chart">
            <img class="graphic-big" src="../assets/graphic-big.jpg" alt="" />
            <img
              class="graphic-desktop"
              src="../assets/graphic-desktop.jpg"
              alt=""
            />
            <img class="graphic-mob" src="../assets/chart_mob.jpg" alt="" />
          </div>
        </q-tab-panel>
        <q-tab-panel name="clicks">
          <div class="chart">
            <img class="graphic-big" src="../assets/graphic-big.jpg" alt="" />
            <img
              class="graphic-desktop"
              src="../assets/graphic-desktop.jpg"
              alt=""
            />
            <img class="graphic-mob" src="../assets/chart_mob.jpg" alt="" />
          </div>
        </q-tab-panel>
        <q-tab-panel name="uniqclicks">
          <div class="chart">
            <img class="graphic-big" src="../assets/graphic-big.jpg" alt="" />
            <img
              class="graphic-desktop"
              src="../assets/graphic-desktop.jpg"
              alt=""
            />
            <img class="graphic-mob" src="../assets/chart_mob.jpg" alt="" />
          </div>
        </q-tab-panel>
        <q-tab-panel name="ctr">
          <div class="chart">
            <img class="graphic-big" src="../assets/graphic-big.jpg" alt="" />
            <img
              class="graphic-desktop"
              src="../assets/graphic-desktop.jpg"
              alt=""
            />
            <img class="graphic-mob" src="../assets/chart_mob.jpg" alt="" />
          </div>
        </q-tab-panel>
        <q-tab-panel name="cpm">
          <div class="chart">
            <img class="graphic-big" src="../assets/graphic-big.jpg" alt="" />
            <img
              class="graphic-desktop"
              src="../assets/graphic-desktop.jpg"
              alt=""
            />
            <img class="graphic-mob" src="../assets/chart_mob.jpg" alt="" />
          </div>
        </q-tab-panel>
      </q-tab-panels>
    </q-card>

    <q-markup-table flat :class="{ lock: lockPage }">
      <thead>
        <tr>
          <th class="text-left">
            <span @click="sorted.date = !sorted.date"
              >Дата
              <span
                class="sorting" :class="{ sorted: sorted.date }">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7.85387 6.14482C7.85387 5.76546 8.17174 5.45793 8.56385 5.45793H22.29C22.6821 5.45793 23 5.76546 23 6.14482C23 6.52418 22.6821 6.83172 22.29 6.83172H8.56385C8.17174 6.83172 7.85387 6.52418 7.85387 6.14482Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 8.8924C7.85387 8.51304 8.17174 8.20551 8.56385 8.20551H19.9234C20.3156 8.20551 20.6334 8.51304 20.6334 8.8924C20.6334 9.27176 20.3156 9.57929 19.9234 9.57929H8.56385C8.17174 9.57929 7.85387 9.27176 7.85387 8.8924Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 11.64C7.85387 11.2606 8.17174 10.9531 8.56385 10.9531H15.6636C16.0557 10.9531 16.3736 11.2606 16.3736 11.64C16.3736 12.0193 16.0557 12.3269 15.6636 12.3269H8.56385C8.17174 12.3269 7.85387 12.0193 7.85387 11.64Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 14.3876C7.85387 14.0082 8.17174 13.7007 8.56385 13.7007H11.8771C12.2692 13.7007 12.587 14.0082 12.587 14.3876C12.587 14.7669 12.2692 15.0744 11.8771 15.0744H8.56385C8.17174 15.0744 7.85387 14.7669 7.85387 14.3876Z"
                    fill="#596982"
                  />
                  <path
                    d="M3.12071 5.68689C3.12071 5.30753 3.43858 5 3.83068 5C4.22279 5 4.54066 5.30753 4.54066 5.68689V15.7613C4.54066 16.1407 4.22279 16.4482 3.83068 16.4482C3.43858 16.4482 3.12071 16.1407 3.12071 15.7613V5.68689Z"
                    fill="#596982"
                  />
                  <path
                    d="M4.16848 18.8628C3.98295 19.0457 3.67842 19.0457 3.49289 18.8628L1.13647 16.54C0.842582 16.2503 1.05471 15.7613 1.47426 15.7613L6.1871 15.7613C6.60666 15.7613 6.81878 16.2503 6.5249 16.54L4.16848 18.8628Z"
                    fill="#596982"
                  />
                </svg>
              </span>
            </span>
          </th>
          <th class="text-left">
            <span @click="sorted.shows = !sorted.shows"
              >Показы
              <span class="sorting" :class="{ sorted: sorted.shows }">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7.85387 6.14482C7.85387 5.76546 8.17174 5.45793 8.56385 5.45793H22.29C22.6821 5.45793 23 5.76546 23 6.14482C23 6.52418 22.6821 6.83172 22.29 6.83172H8.56385C8.17174 6.83172 7.85387 6.52418 7.85387 6.14482Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 8.8924C7.85387 8.51304 8.17174 8.20551 8.56385 8.20551H19.9234C20.3156 8.20551 20.6334 8.51304 20.6334 8.8924C20.6334 9.27176 20.3156 9.57929 19.9234 9.57929H8.56385C8.17174 9.57929 7.85387 9.27176 7.85387 8.8924Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 11.64C7.85387 11.2606 8.17174 10.9531 8.56385 10.9531H15.6636C16.0557 10.9531 16.3736 11.2606 16.3736 11.64C16.3736 12.0193 16.0557 12.3269 15.6636 12.3269H8.56385C8.17174 12.3269 7.85387 12.0193 7.85387 11.64Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 14.3876C7.85387 14.0082 8.17174 13.7007 8.56385 13.7007H11.8771C12.2692 13.7007 12.587 14.0082 12.587 14.3876C12.587 14.7669 12.2692 15.0744 11.8771 15.0744H8.56385C8.17174 15.0744 7.85387 14.7669 7.85387 14.3876Z"
                    fill="#596982"
                  />
                  <path
                    d="M3.12071 5.68689C3.12071 5.30753 3.43858 5 3.83068 5C4.22279 5 4.54066 5.30753 4.54066 5.68689V15.7613C4.54066 16.1407 4.22279 16.4482 3.83068 16.4482C3.43858 16.4482 3.12071 16.1407 3.12071 15.7613V5.68689Z"
                    fill="#596982"
                  />
                  <path
                    d="M4.16848 18.8628C3.98295 19.0457 3.67842 19.0457 3.49289 18.8628L1.13647 16.54C0.842582 16.2503 1.05471 15.7613 1.47426 15.7613L6.1871 15.7613C6.60666 15.7613 6.81878 16.2503 6.5249 16.54L4.16848 18.8628Z"
                    fill="#596982"
                  />
                </svg>
              </span>
            </span>
          </th>
          <th class="text-left">
            <span @click="sorted.clicks = !sorted.clicks"
              >Клики
              <span class="sorting" :class="{ sorted: sorted.clicks }">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7.85387 6.14482C7.85387 5.76546 8.17174 5.45793 8.56385 5.45793H22.29C22.6821 5.45793 23 5.76546 23 6.14482C23 6.52418 22.6821 6.83172 22.29 6.83172H8.56385C8.17174 6.83172 7.85387 6.52418 7.85387 6.14482Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 8.8924C7.85387 8.51304 8.17174 8.20551 8.56385 8.20551H19.9234C20.3156 8.20551 20.6334 8.51304 20.6334 8.8924C20.6334 9.27176 20.3156 9.57929 19.9234 9.57929H8.56385C8.17174 9.57929 7.85387 9.27176 7.85387 8.8924Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 11.64C7.85387 11.2606 8.17174 10.9531 8.56385 10.9531H15.6636C16.0557 10.9531 16.3736 11.2606 16.3736 11.64C16.3736 12.0193 16.0557 12.3269 15.6636 12.3269H8.56385C8.17174 12.3269 7.85387 12.0193 7.85387 11.64Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 14.3876C7.85387 14.0082 8.17174 13.7007 8.56385 13.7007H11.8771C12.2692 13.7007 12.587 14.0082 12.587 14.3876C12.587 14.7669 12.2692 15.0744 11.8771 15.0744H8.56385C8.17174 15.0744 7.85387 14.7669 7.85387 14.3876Z"
                    fill="#596982"
                  />
                  <path
                    d="M3.12071 5.68689C3.12071 5.30753 3.43858 5 3.83068 5C4.22279 5 4.54066 5.30753 4.54066 5.68689V15.7613C4.54066 16.1407 4.22279 16.4482 3.83068 16.4482C3.43858 16.4482 3.12071 16.1407 3.12071 15.7613V5.68689Z"
                    fill="#596982"
                  />
                  <path
                    d="M4.16848 18.8628C3.98295 19.0457 3.67842 19.0457 3.49289 18.8628L1.13647 16.54C0.842582 16.2503 1.05471 15.7613 1.47426 15.7613L6.1871 15.7613C6.60666 15.7613 6.81878 16.2503 6.5249 16.54L4.16848 18.8628Z"
                    fill="#596982"
                  />
                </svg>
              </span>
            </span>
          </th>
          <th class="text-left">
            <span @click="sorted.uniqClicks = !sorted.uniqClicks"
              >Ун. клики
              <span class="sorting" :class="{ sorted: sorted.uniqClicks }">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7.85387 6.14482C7.85387 5.76546 8.17174 5.45793 8.56385 5.45793H22.29C22.6821 5.45793 23 5.76546 23 6.14482C23 6.52418 22.6821 6.83172 22.29 6.83172H8.56385C8.17174 6.83172 7.85387 6.52418 7.85387 6.14482Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 8.8924C7.85387 8.51304 8.17174 8.20551 8.56385 8.20551H19.9234C20.3156 8.20551 20.6334 8.51304 20.6334 8.8924C20.6334 9.27176 20.3156 9.57929 19.9234 9.57929H8.56385C8.17174 9.57929 7.85387 9.27176 7.85387 8.8924Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 11.64C7.85387 11.2606 8.17174 10.9531 8.56385 10.9531H15.6636C16.0557 10.9531 16.3736 11.2606 16.3736 11.64C16.3736 12.0193 16.0557 12.3269 15.6636 12.3269H8.56385C8.17174 12.3269 7.85387 12.0193 7.85387 11.64Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 14.3876C7.85387 14.0082 8.17174 13.7007 8.56385 13.7007H11.8771C12.2692 13.7007 12.587 14.0082 12.587 14.3876C12.587 14.7669 12.2692 15.0744 11.8771 15.0744H8.56385C8.17174 15.0744 7.85387 14.7669 7.85387 14.3876Z"
                    fill="#596982"
                  />
                  <path
                    d="M3.12071 5.68689C3.12071 5.30753 3.43858 5 3.83068 5C4.22279 5 4.54066 5.30753 4.54066 5.68689V15.7613C4.54066 16.1407 4.22279 16.4482 3.83068 16.4482C3.43858 16.4482 3.12071 16.1407 3.12071 15.7613V5.68689Z"
                    fill="#596982"
                  />
                  <path
                    d="M4.16848 18.8628C3.98295 19.0457 3.67842 19.0457 3.49289 18.8628L1.13647 16.54C0.842582 16.2503 1.05471 15.7613 1.47426 15.7613L6.1871 15.7613C6.60666 15.7613 6.81878 16.2503 6.5249 16.54L4.16848 18.8628Z"
                    fill="#596982"
                  />
                </svg>
              </span>
            </span>
          </th>
          <th class="text-left">
            <span @click="sorted.ctr = !sorted.ctr"
              >CTR
              <span class="sorting" :class="{ sorted: sorted.ctr }">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7.85387 6.14482C7.85387 5.76546 8.17174 5.45793 8.56385 5.45793H22.29C22.6821 5.45793 23 5.76546 23 6.14482C23 6.52418 22.6821 6.83172 22.29 6.83172H8.56385C8.17174 6.83172 7.85387 6.52418 7.85387 6.14482Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 8.8924C7.85387 8.51304 8.17174 8.20551 8.56385 8.20551H19.9234C20.3156 8.20551 20.6334 8.51304 20.6334 8.8924C20.6334 9.27176 20.3156 9.57929 19.9234 9.57929H8.56385C8.17174 9.57929 7.85387 9.27176 7.85387 8.8924Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 11.64C7.85387 11.2606 8.17174 10.9531 8.56385 10.9531H15.6636C16.0557 10.9531 16.3736 11.2606 16.3736 11.64C16.3736 12.0193 16.0557 12.3269 15.6636 12.3269H8.56385C8.17174 12.3269 7.85387 12.0193 7.85387 11.64Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 14.3876C7.85387 14.0082 8.17174 13.7007 8.56385 13.7007H11.8771C12.2692 13.7007 12.587 14.0082 12.587 14.3876C12.587 14.7669 12.2692 15.0744 11.8771 15.0744H8.56385C8.17174 15.0744 7.85387 14.7669 7.85387 14.3876Z"
                    fill="#596982"
                  />
                  <path
                    d="M3.12071 5.68689C3.12071 5.30753 3.43858 5 3.83068 5C4.22279 5 4.54066 5.30753 4.54066 5.68689V15.7613C4.54066 16.1407 4.22279 16.4482 3.83068 16.4482C3.43858 16.4482 3.12071 16.1407 3.12071 15.7613V5.68689Z"
                    fill="#596982"
                  />
                  <path
                    d="M4.16848 18.8628C3.98295 19.0457 3.67842 19.0457 3.49289 18.8628L1.13647 16.54C0.842582 16.2503 1.05471 15.7613 1.47426 15.7613L6.1871 15.7613C6.60666 15.7613 6.81878 16.2503 6.5249 16.54L4.16848 18.8628Z"
                    fill="#596982"
                  />
                </svg>
              </span>
            </span>
          </th>
          <th class="text-left">
            <span @click="sorted.cpm = !sorted.cpm"
              >CPM
              <span class="sorting" :class="{ sorted: sorted.cpm }">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7.85387 6.14482C7.85387 5.76546 8.17174 5.45793 8.56385 5.45793H22.29C22.6821 5.45793 23 5.76546 23 6.14482C23 6.52418 22.6821 6.83172 22.29 6.83172H8.56385C8.17174 6.83172 7.85387 6.52418 7.85387 6.14482Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 8.8924C7.85387 8.51304 8.17174 8.20551 8.56385 8.20551H19.9234C20.3156 8.20551 20.6334 8.51304 20.6334 8.8924C20.6334 9.27176 20.3156 9.57929 19.9234 9.57929H8.56385C8.17174 9.57929 7.85387 9.27176 7.85387 8.8924Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 11.64C7.85387 11.2606 8.17174 10.9531 8.56385 10.9531H15.6636C16.0557 10.9531 16.3736 11.2606 16.3736 11.64C16.3736 12.0193 16.0557 12.3269 15.6636 12.3269H8.56385C8.17174 12.3269 7.85387 12.0193 7.85387 11.64Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 14.3876C7.85387 14.0082 8.17174 13.7007 8.56385 13.7007H11.8771C12.2692 13.7007 12.587 14.0082 12.587 14.3876C12.587 14.7669 12.2692 15.0744 11.8771 15.0744H8.56385C8.17174 15.0744 7.85387 14.7669 7.85387 14.3876Z"
                    fill="#596982"
                  />
                  <path
                    d="M3.12071 5.68689C3.12071 5.30753 3.43858 5 3.83068 5C4.22279 5 4.54066 5.30753 4.54066 5.68689V15.7613C4.54066 16.1407 4.22279 16.4482 3.83068 16.4482C3.43858 16.4482 3.12071 16.1407 3.12071 15.7613V5.68689Z"
                    fill="#596982"
                  />
                  <path
                    d="M4.16848 18.8628C3.98295 19.0457 3.67842 19.0457 3.49289 18.8628L1.13647 16.54C0.842582 16.2503 1.05471 15.7613 1.47426 15.7613L6.1871 15.7613C6.60666 15.7613 6.81878 16.2503 6.5249 16.54L4.16848 18.8628Z"
                    fill="#596982"
                  />
                </svg>
              </span>
            </span>
          </th>
          <th class="text-right">
            <span @click="sorted.profit = !sorted.profit"
              >Доход
              <span class="sorting" :class="{ sorted: sorted.profit }">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7.85387 6.14482C7.85387 5.76546 8.17174 5.45793 8.56385 5.45793H22.29C22.6821 5.45793 23 5.76546 23 6.14482C23 6.52418 22.6821 6.83172 22.29 6.83172H8.56385C8.17174 6.83172 7.85387 6.52418 7.85387 6.14482Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 8.8924C7.85387 8.51304 8.17174 8.20551 8.56385 8.20551H19.9234C20.3156 8.20551 20.6334 8.51304 20.6334 8.8924C20.6334 9.27176 20.3156 9.57929 19.9234 9.57929H8.56385C8.17174 9.57929 7.85387 9.27176 7.85387 8.8924Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 11.64C7.85387 11.2606 8.17174 10.9531 8.56385 10.9531H15.6636C16.0557 10.9531 16.3736 11.2606 16.3736 11.64C16.3736 12.0193 16.0557 12.3269 15.6636 12.3269H8.56385C8.17174 12.3269 7.85387 12.0193 7.85387 11.64Z"
                    fill="#596982"
                  />
                  <path
                    d="M7.85387 14.3876C7.85387 14.0082 8.17174 13.7007 8.56385 13.7007H11.8771C12.2692 13.7007 12.587 14.0082 12.587 14.3876C12.587 14.7669 12.2692 15.0744 11.8771 15.0744H8.56385C8.17174 15.0744 7.85387 14.7669 7.85387 14.3876Z"
                    fill="#596982"
                  />
                  <path
                    d="M3.12071 5.68689C3.12071 5.30753 3.43858 5 3.83068 5C4.22279 5 4.54066 5.30753 4.54066 5.68689V15.7613C4.54066 16.1407 4.22279 16.4482 3.83068 16.4482C3.43858 16.4482 3.12071 16.1407 3.12071 15.7613V5.68689Z"
                    fill="#596982"
                  />
                  <path
                    d="M4.16848 18.8628C3.98295 19.0457 3.67842 19.0457 3.49289 18.8628L1.13647 16.54C0.842582 16.2503 1.05471 15.7613 1.47426 15.7613L6.1871 15.7613C6.60666 15.7613 6.81878 16.2503 6.5249 16.54L4.16848 18.8628Z"
                    fill="#596982"
                  />
                </svg>
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
          <td class="text-left total">Итого</td>
          <td class="text-left total">98</td>
          <td class="text-left total">58</td>
          <td class="text-left total">554</td>
          <td class="text-left total">400.66</td>
          <td class="text-left total">258.33</td>
          <td class="text-right total">380.88 ₽</td>
        </tr>
      </tbody>
    </q-markup-table>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      datepicker: false,
      filter: false,
      sorted: {
        date: false,
        shows: false,
        clicks: false,
        uniqClicks: false,
        ctr: false,
        cpm: false,
        profit: false
      },
      chartToggle: false,
      dateOne: { from: "2021/01/04", to: "2021/01/10" },
      dateTwo: "2021/02/01",
      group: null,
      groupOptions: ["Дата", "Сайт", "Блок", "Страна", "Платформа"],
      groupCheckbox: [true, false, false, false, false],
      filterOne: null,
      optionsOne: ["Сайт", "Блок", "Страна", "Платформа"],
      filterTwo: null,
      optionsTwo: [
        "website#1.com",
        "Значение 1",
        "Значение 2",
        "Значение 3",
        "Значение 4"
      ],
      filterThree: null,
      optionsThree: ["Сайт", "Блок", "Страна", "Платформа"],
      filterFour: null,
      optionsFour: [
        "website#1.com",
        "Значение 1",
        "Значение 2",
        "Значение 3",
        "Значение 4"
      ],
      tabCharts: "profit",
      lockPage: false
    };
  },
  methods: {
    createValue (val, done) {
      if (val.length > 0) {
        if (!this.optionsTwo.includes(val)) {
          this.optionsTwo.push(val)
        }
        done(val, 'toggle')
      }
    }
  }
};
</script>

<style lang="scss">
.q-page {
  padding: 40px;

  @media (max-width: 1366px) {
    padding: 32px 40px;
  }

  @media (max-width: 1200px) {
    padding: 32px;
  }
}

.statistics-page {
  &.lock {
    position: fixed;
    width: calc(100% - 253px);

    @media (max-width:1600px){
      width: calc(100% - 112px);
    }
  }

  .title-mob {
    display: none;
  }

  .filters {
    margin: 0px 0px 40px 0px;

    @media (max-width: 1366px) {
      margin: 0px 0px 32px 0px;
    }

    .q-btn {
      margin: 0px 24px 0px 0px;

      @media (max-width: 1144px) {
        margin: 0px 24px 10px 0px;
      }
    }
  }

  [aria-expanded="true"] {
    border: 1px solid #596982 !important;
  }

  .q-btn + .q-btn {
    margin: 0px 0px 0px 24px;
  }

  .datepicker {
    color: #12284c;
    border: 1px solid #a0a9b7;
    box-sizing: border-box;
    border-radius: 4px;
    font-size: 16px;
    line-height: 20px;
    letter-spacing: -0.15px;
    position: relative;
    transition: all 0.3s;
    margin: 0px 24px 0px 0px;

    &:hover {
      border: 1px solid #596982;
    }

    .q-btn__wrapper {
      padding: 10px 15px 8px 63px;
      min-height: 0px;
    }

    .q-focus-helper,
    i,
    .q-btn__wrapper:before {
      display: none;
    }

    &::after {
      content: "";
      position: absolute;
      width: 24px;
      height: 24px;
      top: 7px;
      left: 15px;
      background: url("../assets/calendar.svg") 0 0 no-repeat;
    }
  }

  .q-field {
    margin: 0px 24px 0px 0;
    border: 1px solid #a0a9b7;
    box-sizing: border-box;
    border-radius: 4px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
    padding-bottom: 8px;

    &:hover {
      border: 1px solid #596982;
    }

    &--focused {
      border: 1px solid #596982;

      .q-field__label {
        display: none;
      }
    }

    &--float {
      .q-field__label {
        display: none;
      }
    }

    &__control {
      height: 40px;
      min-height: 0;
      padding: 0 16px;

      &::after {
        height: 0;
      }
    }

    &__append {
      height: 40px;
    }

    &__control-container {
      padding-top: 0px !important;
    }

    &__label {
      color: #a0a9b7;
      font-weight: 500;
      top: 10px;
      font-size: 16px;
      line-height: 20px;
      letter-spacing: -0.15px;
    }

    &__native {
      min-height: 0 !important;
      font-size: 16px;
      line-height: 20px;
      color: #12284c;
      font-weight: 500;
      padding: 8px 0px 0px 0px;

      span {
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }

      .no-outline {
        display: none;
      }
    }

    .q-select__dropdown-icon {
      font-size: 24px;
      margin: -5px -10px -2px 0px;
      color: #4690ff;
    }

    @media (max-width: 1144px) {
      margin: 0px 24px 10px 0;
    }
  }

  .q-field--filled .q-field__control {
    background: transparent;
  }

  .q-field--filled .q-field__control:before {
    background: transparent !important;
    border-bottom: none;
  }

  .filter {
    color: #12284c;
    border: 1px solid #a0a9b7;
    box-sizing: border-box;
    border-radius: 4px;
    font-size: 16px;
    line-height: 20px;
    letter-spacing: -0.15px;
    transition: all 0.3s;
    position: relative;

    &:hover {
      border: 1px solid #596982;
    }

    &__wrp {
      position: relative;
    }

    .q-btn__wrapper {
      padding: 10px 15px 8px 63px;
      min-height: 0px;
    }

    .q-focus-helper,
    i,
    .q-btn__wrapper:before {
      display: none;
    }

    &::after {
      content: "";
      position: absolute;
      width: 24px;
      height: 24px;
      top: 7px;
      left: 15px;
      background: url("../assets/filter.svg") 0 0 no-repeat;
      z-index: 2;
    }

    &.active {
      &::after {
        background: #4690ff;
        border-radius: 50%;
      }
    }
  }

  .filter-counter {
    position: absolute;
    width: 24px;
    height: 24px;
    top: 11px;
    left: 16px;
    z-index: 1;
    color: #fff;
    text-align: center;
    font-size: 16px;
    line-height: 20px;

    &.active {
      z-index: 3;
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
  }

  .chart-toggle {
    margin: 0px 54px 0px auto;

    @media (min-width:501px){
      &:hover{
        .q-toggle__track {
          border: 1px solid #4690ff !important;
          opacity: 1;
        }
      }      
    }

    .q-toggle__track {
      transition: all 0.3s;
      height: 24px;
      width: 40px;
      border-radius: 500px;
      opacity: 0.38;
      background: transparent;
      border: 1px solid #5a6577;
    }

    .q-toggle__label {
      font-size: 16px;
      color: #12284c;
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
        background-color: #4690ff;
      }

      .q-toggle__track {
        border: 1px solid #4690ff !important;
        opacity: 1;
      }
    }

    .q-toggle__thumb {
      width: 16px;
      height: 16px;
    }

    .q-toggle__thumb::after {
      background: #a0a9b7;
      width: 16px;
      height: 16px;
      top: 2px;
      box-shadow: none;
    }

    .q-toggle__thumb:before {
      display: none;
    }

    @media (max-width: 1150px) {
      margin: 0px 54px 0px 0px;
    }
  }

  .cvs-icon {
    cursor: pointer;
    display: flex;
    align-self: center;
    transition: all 0.3s;

    &:hover{
      svg {
        [fill = "#596982"] {
          transition: all 0.3s;
          fill: #12284C;
        }
      }
    }
  }

  .q-markup-table {
    box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
    border-radius: 4px;

    .q-table {
      padding: 24px 24px 9px;
      width: 0;
      min-width: 100%;

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
          // min-width: 240px;
          max-width: 240px;
          width: 15.9%;

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

            &:hover {
              svg {
                path {
                  fill: #12284c;
                }
              }
            }

            &.sorted {
              svg {
                path {
                  fill: #4690ff !important;
                }
              }
            }

            @media (max-width: 1200px) {
              top: -4px;
              right: -7px;
            }
          }

          @media (max-width: 1366px) {
            max-width: 107.71px;
            width: 15.3%;
          }

          @media (max-width: 1200px) {
            font-size: 16px;
            padding: 4px 0 18px 0px;
            width: 14.65%;
          }

          @media (max-width: 1100px) {
            min-width: 128px;
          }
        }

        .text-right {
          min-width: 96px;

          @media (max-width: 1366px) {
            span {
              padding: 0px 47px 0px 0px;
            }
          }

          @media (max-width: 1200px) {
            span {
              padding: 0px 64px 0px 0px;
            }
          }
        }
      }

      tbody {
        td {
          font-size: 18px;
          line-height: 22px;
          padding: 16px 0px 15px 0px;
          height: 54px;
          // min-width: 240px;
          max-width: 240px;
          width: 15.9%;

          &:before {
            background: transparent;
          }

          @media (max-width: 1200px) {
            font-size: 16px;
            width: 14.65%;
          }

          @media (max-width: 1100px) {
            min-width: 128px;
          }
        }

        .text-right {
          min-width: 96px;
          color: #95bd5a;
          padding: 0px 16px 0px 0px;

          @media (max-width: 1366px) {
            padding: 0px 29px 0px 0px;
          }

          @media (max-width: 1200px) {
            padding: 2px 50px 0px 0px;
          }
        }

        .total {
          font-weight: 500;
        }
      }
    }
  }

  .q-card {
    padding: 24px;
    background-color: #fff;
    margin: 0px 0px 40px 0px;
    box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
    border-radius: 4px;

    @media (max-width: 1366px) {
      margin: 0px 0px 32px 0px;
    }

    .scroll {
      overflow: hidden !important;
    }

    .q-tabs {
      display: flex;
      margin: 0px 0px 27px 0px;
      padding: 2px 0px 0px 0px;

      @media (max-width: 1366px) {
        padding: 5px 0px 0px 0px;
        margin: 0px 0px 28px 0px;
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
      margin: 3px 0px 0px 0px;

      .q-focus-helper {
        display: none;
      }

      &-panel {
        padding: 0;

        .chart__mob {
          display: none;
        }

        .chart {
          position: relative;
          overflow: hidden;

          .graphic-big {
            display: block;
          }

          .graphic-desktop,
          .graphic-mob {
            display: none;
          }

          @media (max-width: 1366px) {
            .graphic-desktop {
              display: block;
            }

            .graphic-big {
              display: none;
            }
          }
        }
      }

      &__label {
        color: #596982;
        font-size: 18px;
        line-height: 25px;

        &:hover {
          color: #12284c !important;
        }

        @media (max-width: 1360px) {
          font-size: 16px;
          line-height: 20px;
        }
      }

      & + .q-tab {
        margin: 0px 0px 0px 31px;

        @media (max-width: 700px) {
          margin: 0px 0px 0px 14px;
        }
      }

      &--active {
        position: relative;
        color: #12284c !important;

        .q-tab__label {
          color: #12284c !important;
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

      @media (max-width: 1366px) {
        margin: 0;
      }
    }

    .chart {
      width: 1539px;
      height: 432px;
      position: relative;

      img {
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        object-fit: cover;
        object-position: 0 0;
      }

      @media (max-width: 1366px) {
        height: 297px;
        width: 1146px;
      }
    }
  }
}

.q-virtual-scroll__content {
  .q-item {
    min-height: 0;
    position: relative;
    padding: 10px 24px 9px;

    &:hover {
      background: #f3f4f6;
    }

    &__label {
      color: #12284c;
    }

    .q-focus-helper {
      display: none;
    }
  }
}

.q-menu {
  &.datepicker-popup {
    min-height: 493px;

    .datepicker-list {
      margin: 1px 48px 0px 0px;
      padding: 0px 0px 17px 0px;
      min-width: 140px;

      @media (max-width: 1130px) {
        margin: 1px 0px 0px 0px;
      }

      .datepicker-listitem {
        cursor: pointer;
        font-size: 14px;
        line-height: 17px;
        color: #596982;
        position: relative;

        &:hover{
          color: #12284c;
        }

        @media (max-width: 1130px) {
          color: #12284c;
        }

        & + .datepicker-listitem {
          margin: 25px 0px 0px 0px;

          @media (max-width: 1130px) {
            margin: 0px 16px 16px 0px;
          }
        }

        &.active {
          color: #4690ff;

          &::after {
            content: "";
            position: absolute;
            width: 2px;
            height: 18px;
            top: 0;
            right: -2px;
            background-color: #4690ff;

            @media (max-width: 1130px) {
              display: none;
            }
          }

          @media (max-width: 1130px) {
            color: #12284c;
            border: none;
            background: #f0f5fd;
            border: 1px solid #f0f5fd;
          }
        }

        @media (max-width: 1130px) {
          display: inline-block;
          padding: 3px 8px;
          border: 1px solid #a0a9b7;
          border-radius: 50px;
          margin: 0px 16px 16px 0px;
        }
      }
    }

    .datepicker-menu {
      display: flex;
      position: relative;
      padding: 40px;

      .q-date {
        width: 322px;

        & + .q-date {
          margin: 0px 0px 0px 40px;

          @media (max-width: 900px) {
            margin: 40px auto 0px;
          }
        }

        box-shadow: none;
        min-width: 322px;

        &__navigation {
          height: 17px;
          margin: 0px auto 33px;
          max-width: 240px;

          .q-ripple {
            display: none;
          }

          .q-date__arrow + .q-date__arrow {
            padding: 0px 0px 0px 21px;
          }

          .q-date__arrow {
            .q-btn .q-icon,
            .q-btn .q-spinner {
              font-size: 23px;
              color: #596982;
              
              @media (min-width:501px){
                &:hover{
                  color: #12284c;
                }                
              }
            }

            .q-focus-helper {
              display: none;
            }
          }

          .q-btn {
            .q-focus-helper {
              display: none;
            }
          }

          .q-btn__content .block {
            margin: 0 6px;
            color: #596982;

            &:hover{
              color: #12284c;
            }
          }
        }

        &__calendar-weekdays {
          height: 46px;

          .q-date__calendar-item {
            &:hover {
              background-color: #fff;
              cursor: default;
            }
          }
        }

        &__header,
        &__actions {
          display: none;
        }

        &__view,
        &__calendar-days-container {
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
          color: #12284c;
          border-radius: 4px;

          .q-focus-helper {
            display: none;
          }

          &--in {
            font-weight: 400;
          }

          .block {
            color: #12284c;
          }

          &:hover {
            background: #f0f5fd;
            cursor: pointer;
          }

          button {
            width: 46px;
            height: 46px;
            border-radius: 4px;
          }

          .q-btn {
            &.bg-primary {
              background: #4690ff !important;
              border-radius: 4px;

              .block {
                color: #fff !important;
              }
            }
          }
        }

        &__calendar-days > div {
          height: 46px !important;
          width: 46px !important;
        }

        &__edit-range {
          background-color: #4690ff;
        }

        &__range-from,
        &__edit-range-from,
        &__range-to,
        &__edit-range-to {
          background-color: #4690ff !important;
          border-radius: 4px;

          .q-btn {
            &.bg-primary {
              background: #4690ff !important;
            }
          }

          .q-focus-helper {
            display: none;
          }

          .block {
            color: #fff;
          }
        }

        &__today {
          background-color: #f0f5fd !important;
          border-radius: 4px;
          overflow: hidden;
          box-shadow: none;

          .q-btn {
            &.bg-primary {
              background: #f0f5fd !important;
            }
          }

          .q-focus-helper {
            display: none;
          }

          .block {
            color: #12284c;
          }
        }

        &__range-from:before,
        &__range-to:before {
          display: none;
        }

        &__range:before {
          background: #d4e4fe;
        }

        &__months-item,
        &__years-item {
          .block {
            color: #12284c !important;
          }
          .q-btn {
            box-shadow: none !important;
          }
        }

        @media (max-width: 900px) {
          display: flex;
          justify-content: center;
          margin: 0 auto;
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
        transition: all 0.3s;

        &:hover {
          color: #12284c;
        }

        @media (max-width: 1360px) {
          bottom: 65px;
        }

        @media (max-width: 1130px) {
          display: none;
        }
      }

      .datepicker-btn-two {
        display: none;
      }

      @media (max-width: 1130px) {
        display: block;
        padding: 16px;
      }
    }

    .datepicker-nav {
      display: none;

      @media (max-width: 1130px) {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0px 0px 27px 0px;

        .datepicker-reset {
          color: #a64541;
          font-weight: 500;
          font-size: 14px;
          line-height: 18px;
        }

        .datepicker-title {
          font-weight: 600;
          font-size: 14px;
          line-height: 18px;
          color: #12284c;
          margin: 0px 50px 0px 0px;
        }

        .datepicker-close {
          cursor: pointer;

          svg {
            path {
              fill: #596982;
            }
          }

          &.active {
            svg {
              path {
                fill: #12284c;
              }
            }
          }
        }
      }
    }

    @media (max-width: 1130px) {
      margin: 16px 32px 0px 0px !important;
      max-width: 740px;
      min-height: 520px;
    }
  }

  .filter-menu {
    background-color: #fff;
    box-shadow: 0px 0px 32px rgba(18, 40, 76, 0.08);
    border-radius: 4px;
    padding: 32px;

    .filter-nav {
      display: none;
    }

    &__row,
    &__buttons {
      display: flex;

      & + .filter-menu__buttons {
        margin: 32px 0px 0px 0px;
      }

      & + .filter-menu__row {
        margin: 24px 0px 0px 0px;
      }
    }

    &__buttons {
      flex-wrap: wrap;
      margin: 32px 0px 0px 0px;
    }

    &__close {
      display: flex;
      align-items: center;
      margin: 0px 0px 0px 24px;
      cursor: pointer;

      svg {
        path {
          transition: all 0.3s;
          fill: #B8BFC9;
        }
      }

      &.active{
        path {
          transition: all 0.3s;
          fill: #596982;
        }
      }

      &:hover {
        svg {
          path {
            fill: #12284c;
          }
        }
      }
    }

    .q-field {
      border: 1px solid #a0a9b7;
      box-sizing: border-box;
      border-radius: 4px;
      position: relative;
      overflow: hidden;
      transition: all 0.3s;
      padding-bottom: 8px;

      &:hover {
        border: 1px solid #596982;
      }

      & + .q-field {
        margin: 0px 0px 0px 24px;
      }

      &--focused {
        .q-field__label {
          display: none;
        }
      }

      &--float {
        .q-field__label {
          display: none;
        }
      }

      &__control {
        height: 40px;
        min-height: 0;
        padding: 0 16px;
      }

      &__append {
        height: 40px;
      }

      &__control-container {
        padding-top: 0px !important;
      }

      &__label {
        color: #a0a9b7;
        font-weight: 500;
        top: 10px;
        font-size: 16px;
        line-height: 20px;
        letter-spacing: -0.15px;
      }

      &__native {
        min-height: 0 !important;
        font-size: 16px;
        line-height: 20px;
        color: #12284c;
        font-weight: 500;
        padding: 0px 0px 0px 0px;
        flex-wrap: nowrap;
        overflow: hidden;

        span {
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }

        .no-outline {
          display: none;
        }

        .q-chip {
          padding: 4px 10px 4px 3px;
          height: 28px;
          margin: 0;
          border-radius: 4px;
          background: #dbdfe4;
          z-index: 1;

          & + .q-chip {
            margin: 0px 0px 0px 5px;
          }

          &__content {
            .ellipsis {
              color: #12284c;
              font-size: 16px;
              line-height: 20px;
              letter-spacing: -0.2px;
            }
          }

          &__icon {
            color: transparent;
            position: relative;

            &::after {
              content: "";
              position: absolute;
              width: 16px;
              height: 16px;
              top: 0px;
              right: -2px;
              background: url("../assets/close.svg") 0 0 no-repeat;
            }
          }
        }
      }

      .q-select__dropdown-icon {
        font-size: 24px;
        margin: -5px -10px -2px 0px;
        color: #4690ff;
      }
    }

    .q-field--filled .q-field__control {
      background: transparent;
    }

    .q-field--filled .q-field__control:before {
      background: transparent !important;
      border-bottom: none;
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

      &-white {
        transition: all 0.1s;
        color: #4690ff;
        background: #fff;
        border: 1px solid #4690ff;
        box-sizing: border-box;
        border-radius: 4px;
        margin: 0px 24px 0px 1px;
        transition: all 0.5s;

        &:hover {
          background: #F3F4F6;
        }

        &:active {
          background: #fff !important;
          color: #fff;
          box-shadow: none;
        }

        .q-ripple {
          background: #fff !important;
          position: absolute;
          z-index: 0 !important;
          overflow: hidden;
        }
      }

      &-blue {
        color: #fff;
        background-color: #4690ff;
        border: 1px solid #4690ff;
        box-sizing: border-box;
        border-radius: 4px;
        margin: 0px 24px 0px auto;

        &:active {
          background-color: transparent;
          color: #fff;
          box-shadow: none;
          background-color: #4690ff;
        }

        @media (max-width: 800px) {
          margin: 0px 24px 0px 0;
        }
      }

      &-red {
        color: #b36f6c;
        background-color: #fff;
        margin: 0px 24px 0px 0px;

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

      &.btn-reset {
        display: block;
      }

      &.btn-del {
        display: none;
      }

      @media (max-width: 800px) {
        margin: 0px 24px 10px 0px;
      }
    }

    .q-btn {
      .block {
        white-space: nowrap;
      }
    }
  }

  &.group-popup {
    min-width: 213px !important;
    padding: 16px 0;

    .q-item {
      padding: 11px 24px 8px 64px;
      min-height: 0;
      position: relative;

      &:hover {
        background: #f3f4f6;
      }

      &__label {
        color: #12284c;
      }

      .q-focus-helper {
        display: none;
      }

      &::before {
        content: "";
        position: absolute;
        width: 24px;
        height: 24px;
        top: 8px;
        left: 24px;
        background: url("../assets/checkbox-default.svg") 0 0 no-repeat;
      }

      &--active {
        color: #12284c;
        &::before {
          background: url("../assets/checkbox-active.svg") 0 0 no-repeat;
        }
      }
    }

    .group-menu,
    .group-btn {
      display: none;
    }
  }

  &.filterOne {
    min-width: 217px !important;
    padding: 0;

    .q-item {
      padding: 10px 24px 9px;
      min-height: 0;
      position: relative;

      &:hover {
        background: #f3f4f6;
      }

      &__label {
        color: #12284c;
      }

      .q-focus-helper {
        display: none;
      }

      &--active {
        .q-item__label {
          color: #12284c !important;
        }
      }

      &::before {
        display: none !important;
      }
    }
  }

  &.filterTwo {
    min-width: 401px !important;

    .q-item {
      position: relative;
      font-size: 16px;
      line-height: 20px;
      padding: 11px 40px 12px 24px;

      &::after {
        content: "";
        position: absolute;
        top: 9px;
        right: 16px;
        width: 24px;
        height: 24px;
        background: url("../assets/checkbox-default.svg") 0 0 no-repeat;
      }

      &--active {
        &::after {
          background: url("../assets/checkbox-active.svg") 0 0 no-repeat;
        }
      }

      &:hover {
        background-color: #fff;
      }
    }
  }

  &.filter-popup {
    margin: 8px 0px 0px 0px !important;
  }
}

// Mobile
@media (max-width: 500px) {
  .q-page {
    padding: 16px !important;
  }

  .statistics-page {
    max-width: 100%;
    transition: all 0.2s;
    transition-delay: 0s;

    &.lock {
      background: #12284c20;
      position: fixed;
      width: 100%;
    }

    .datepicker {
      &:hover {
        border: 1px solid #a0a9b7;
      }
    }

    .q-field {
      &:hover {
        border: 1px solid #a0a9b7;
      }
    }

    .title-mob {
      display: block;
      font-weight: 500;
      font-size: 24px;
      line-height: 29px;
      color: #12284c;
      margin: 0px 0px 18px 0px;
    }

    .filters {
      margin: 0px 0px 23px 0px;

      .q-btn {
        margin: 0px 0px 16px 0px;
        min-width: 100%;
        font-size: 16px;
      }

      .datepicker,
      .filter {
        .q-btn__content {
          justify-content: flex-start;
        }

        &:hover {
          border: 1px solid #a0a9b7;
        }
      }

      .q-field {
        margin: 0px 0px 16px 0px;
        min-width: 100%;
      }

      .cvs-icon {
        display: none;
      }
    }

    .filter__wrp {
      min-width: 100%;
      margin: 0px 0px 9px 0px;
    }

    .chart-toggle {
      margin: 7px 54px 0px 0px;
      display: flex;
      min-width: 100%;
      justify-content: space-between;

      .q-toggle__inner {
        width: 46px;
      }

      .q-toggle__track {
        &:hover {
          border: 1px solid #5a6577;
        }
      }
    }

    .q-markup-table {
      margin: 0px -16px 73px 0px;
      transition: all 0.2s;

      &.lock {
        background: #464b5712;
        position: fixed;
      }

      .q-table {
        padding: 16px;

        thead {
          tr {
            height: 0px;
          }

          th {
            padding: 4px 0 11px 0px;
            font-size: 14px;
            line-height: 18px;
            color: #596982;
            letter-spacing: 0.03em;
            max-width: 240px;
            width: 15.9%;
            min-width: 122px;

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
              top: 1px;
              right: -8px;

              &:hover {
                svg {
                  path {
                    fill: #596982;
                  }
                }
              }

              svg {
                width: 16px;
                height: 16px;
              }
            }
          }

          .text-right {
            min-width: 96px;

            span {
              padding: 0px 35px 0px 0px;
            }
          }
        }

        tbody {
          td {
            font-size: 14px;
            line-height: 22px;
            padding: 8px 0px 7px 0px;
            height: 38px;
            max-width: 240px;
            width: 15.9%;

            &:before {
              background: transparent;
            }

            min-width: 122px;
          }

          .text-right {
            min-width: 96px;
            color: #95bd5a;
            padding: 2px 15px 0px 0px;
          }

          .total {
            font-weight: 500;
          }
        }
      }
    }

    .q-card {
      box-shadow: none;
      margin: 0 -16px -12px;
      padding: 0px;

      .scroll {
        overflow: hidden !important;
      }

      .q-tab + .q-tab {
        margin: 0px 0px 0px 15px;
      }

      .q-tab {
        &-panel {
          padding: 0;

          .chart {
            height: 262px;
            width: 360px;
            margin: 1px 0px 0px 0px;

            .graphic-desktop {
              display: none;
            }

            .graphic-mob {
              display: block;
            }

            img {
              object-fit: contain;
            }
          }
        }
      }

      .q-tabs {
        padding: 8px 16px 0;
        margin: 0px 0px 22px 0px;

        &__content {
          overflow: auto !important;

          .q-tab {
            &__label {
              font-size: 14px;
            }
          }
        }
      }
    }
  }

  .q-menu {
    &.datepicker-popup {
      position: fixed !important;
      top: 0px !important;
      left: 0px !important;
      min-height: 100% !important;
      margin: 55px 0 0 0 !important;
      padding: 0px 0px 125px 0px !important;
      max-width: 740px !important;
      min-height: 520px !important;
      max-height: 100% !important;
      z-index: 4000;

      .datepicker-list {
        padding: 0px 0px 19px 0px;
        min-width: 140px;
        margin: 48px 0px 0px 0px;

        .datepicker-listitem {
          cursor: pointer;
          font-size: 14px;
          line-height: 17px;
          position: relative;
          display: inline-block;
          padding: 3px 7px 2px 8px;
          border: 1px solid #a0a9b7;
          border-radius: 50px;
          margin: 0px 13px 16px 0px;
          color: #12284c;

          & + .datepicker-listitem {
            margin: 0px 16px 16px 0px;
          }

          &.active {
            color: #12284c;
            border: none;
            background: #f0f5fd;
            border: 1px solid #f0f5fd;

            &::after {
              content: "";
              position: absolute;
              width: 2px;
              height: 18px;
              top: 0;
              right: -2px;
              background-color: #4690ff;
            }
          }
        }
      }

      .datepicker-menu {
        display: block;
        padding: 8px 16px;

        .q-date {
          width: 329px;

          & + .q-date {
            margin: 19px auto 0px;
          }

          box-shadow: none;
          min-width: 322px;

          &__navigation {
            height: 17px;
            margin: 0px auto 11px;
            max-width: 240px;

            .q-date__arrow + .q-date__arrow {
              padding: 0px 0px 0px 21px;
            }

            .q-date__arrow {
              .q-btn .q-icon,
              .q-btn .q-spinner {
                font-size: 23px;
              }

              .q-focus-helper {
                display: none;
              }
            }

            .q-btn {
              .q-focus-helper {
                display: none;
              }
            }

            .q-btn__content .block {
              margin: 0 6px;
            }
          }

          &__calendar-weekdays {
            height: 46px;

            .q-date__calendar-item {
              &:hover {
                background-color: #fff;
                cursor: default;
              }
            }
          }

          &__header,
          &__actions {
            display: none;
          }

          &__view,
          &__calendar-days-container {
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
            color: #12284c;
            border-radius: 4px;

            .q-focus-helper {
              display: none;
            }

            &--in {
              font-weight: 400;
            }

            .block {
              color: #12284c;
            }

            &:hover {
              background: #fff;
              cursor: pointer;
            }

            button {
              width: 46px;
              height: 46px;
              border-radius: 4px;

              @media (max-width: 359px) {
                height: 42px !important;
                width: 42px !important;
              }
            }

            .q-btn {
              &.bg-primary {
                background: #4690ff !important;
                border-radius: 4px;

                .block {
                  color: #fff !important;
                }
              }
            }
          }

          &__calendar-days > div {
            height: 47px !important;
            width: 47px !important;

            @media (max-width: 359px) {
              height: 41px !important;
              width: 41px !important;
            }
          }

          &__edit-range {
            background-color: #4690ff;
          }

          &__range-from,
          &__edit-range-from,
          &__range-to,
          &__edit-range-to {
            background-color: #4690ff !important;
            border-radius: 4px;

            .q-btn {
              &.bg-primary {
                background: #4690ff !important;
              }
            }

            .q-focus-helper {
              display: none;
            }

            .block {
              color: #fff;
            }
          }

          &__today {
            background-color: #f0f5fd !important;
            border-radius: 4px;
            overflow: hidden;
            box-shadow: none;

            .q-btn {
              &.bg-primary {
                background: #f0f5fd !important;
              }
            }

            .q-focus-helper {
              display: none;
            }

            .block {
              color: #12284c;
            }
          }

          &__range-from:before,
          &__range-to:before {
            display: none;
          }

          &__range:before {
            background: #d4e4fe;
          }

          &__months-item,
          &__years-item {
            .block {
              color: #12284c !important;
            }
            .q-btn {
              box-shadow: none !important;
            }
          }

          @media (max-width: 900px) {
            display: flex;
            justify-content: center;
            margin: 0 auto;
          }

          @media (max-width: 359px) {
            width: 288px;
            min-width: 288px;
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
          transition: all 0.3s;

          &:hover {
            color: #12284c;
          }

          @media (max-width: 1130px) {
            display: none;
          }
        }

        .datepicker-btn-two {
          display: block;
          position: fixed;
          width: 100%;
          height: 40px;
          bottom: 16px;
          left: 0;
          color: #fff;
          text-align: center;
          padding: 0 16px;

          span {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100%;
            border-radius: 4px;
            background: #dbdfe4;
            font-size: 16px;

            &.active {
              background: #4690ff;
            }
          }
        }
      }

      .datepicker-nav {
        display: flex !important;
        justify-content: space-between;
        align-items: flex-start;
        margin: -8px 0 0 0;
        padding: 11px 0px 0px 0px;
        position: absolute;
        width: calc(100% - 32px);
        background-color: #fff;
        z-index: 9000;

        .datepicker-reset {
          color: #a64541;
          font-weight: 500;
          font-size: 14px;
          line-height: 18px;
        }

        .datepicker-title {
          font-weight: 600;
          font-size: 14px;
          line-height: 18px;
          color: #12284c;
          margin: 0px 46px 0px 0px;
        }

        .datepicker-close {
          margin: -3px 0px 0px 0px;
          cursor: pointer;

          svg {
            path {
              fill: #596982;
            }
          }

          &.active {
            svg {
              path {
                fill: #12284c;
              }
            }
          }
        }
      }
    }

    &.q-transition--fade-enter-to {
      &.group-popup {
        top: 100% !important;
        transform: translate(0, -100%);
        transition: transform 1s;
        opacity: 1;
        bottom: -256px !important;
        transform: translate(0, -256px);
      }

      &.filter-popup, &.datepicker-popup {
        top: 100% !important;
        transform: translate(0, -100%);
        transition: transform 1s;
        opacity: 1;
        top: 100% !important;
        transform: translate(0, -100%);
      }
    }

    &.q-transition--fade-leave-to {
      &.filter-popup, &.datepicker-popup { 
        top: 0 !important;
        transform: translate(0, 100%);
        transition: transform 1s;
        opacity: 1;
      }

      &.group-popup { 
        bottom: 0 !important;
        transform: translate(0, 256px);
        transition: transform 1s;
        opacity: 1;
      }
    }

    .filter-menu {
      background-color: #fff;
      box-shadow: 0px 0px 32px rgba(18, 40, 76, 0.08);
      border-radius: 4px;
      padding: 9px 16px;
      min-height: 584px;
      box-shadow: none;

      .filter-nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: -5px 0px 20px;
        padding: 0px 0px 0;

        .filter-reset {
          color: #a64541;
          font-weight: 500;
          font-size: 14px;
          line-height: 18px;
        }

        .filter-title {
          font-weight: 600;
          font-size: 14px;
          line-height: 18px;
          color: #12284c;
          margin: 0px 45px 0px 0px;
          letter-spacing: 0.1px;
        }

        .filter-close {
          cursor: pointer;
          margin: 3px 0px 0px 0px;

          svg {
            path {
              fill: #596982;
            }
          }

          &.active {
            svg {
              path {
                fill: #12284c;
              }
            }
          }
        }
      }

      &__row,
      &__buttons {
        display: block;

        & + .filter-menu__buttons {
          margin: 24px 0px 0px 0px;
        }

        & + .filter-menu__row {
          padding: 8px 0px 0px 0px;
        }
      }

      &__buttons {
        flex-wrap: wrap;
        display: flex;
        flex-direction: column-reverse;
        margin: 0;
      }

      &__close {
        display: none;
      }

      .q-field {
        border: 1px solid #a0a9b7;
        box-sizing: border-box;
        border-radius: 4px;
        position: relative;
        overflow: hidden;
        transition: all 0.3s;
        padding-bottom: 8px;
        max-width: 100%;
        min-width: 100%;

        &:hover {
          border: 1px solid #a0a9b7;
        }

        & + .q-field {
          margin: 16px 0px 0px 0px;
        }

        &--focused {
          .q-field__label {
            display: none;
          }
        }

        &--float {
          .q-field__label {
            display: none;
          }
        }

        &__control {
          height: 40px;
          min-height: 0;
          padding: 0 16px;
        }

        &__append {
          height: 40px;
        }

        &__control-container {
          padding-top: 0px !important;
        }

        &__label {
          font-weight: 400;
        }

        &__native {
          min-height: 0 !important;
          font-size: 16px;
          line-height: 20px;
          color: #12284c;
          font-weight: 400;
          padding: 0px 0px 0px 0px;
          flex-wrap: nowrap;
          overflow: hidden;

          span {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
          }

          .no-outline {
            display: none;
          }

          .q-chip {
            padding: 4px 10px 4px 3px;
            height: 28px;
            margin: 0;
            border-radius: 4px;
            background: #dbdfe4;
            z-index: 1;

            & + .q-chip {
              margin: 0px 0px 0px 5px;
            }

            &__content {
              .ellipsis {
                color: #12284c;
                font-size: 16px;
                line-height: 20px;
                letter-spacing: -0.2px;
              }
            }

            &__icon {
              color: transparent;
              position: relative;

              &::after {
                content: "";
                position: absolute;
                width: 16px;
                height: 16px;
                top: 0px;
                right: -2px;
                background: url("../assets/close.svg") 0 0 no-repeat;
              }
            }
          }
        }

        .q-select__dropdown-icon {
          font-size: 24px;
          margin: -5px -10px -2px 0px;
          color: #4690ff;
        }
      }

      .q-field--filled .q-field__control {
        background: transparent;
      }

      .q-field--filled .q-field__control:before {
        background: transparent !important;
        border-bottom: none;
      }

      .btn {
        margin: 0px 24px 10px 0px;
        min-width: 100%;
        font-weight: 500;
        font-size: 16px;
        line-height: 20px;

        .q-ripple {
          display: none;
        }

        &-red {
          color: #b36f6c;
          background-color: #fff;
          margin: 0px 24px 32px 0px;
          border: 1px solid #a64541;
          box-sizing: border-box;
          border-radius: 4px;
          opacity: 0.15;

          .q-btn__wrapper {
            padding: 0;
          }

          &:hover,
          &:active {
            background-color: #fff;
          }

          &.active {
            color: #a64541;
            opacity: 1;
          }
        }

        &-grey {
          display: none;
        }

        &-blue {
          position: fixed;
          bottom: 7px;
          left: 0;
          padding: 0 16px;
          background-color: #fff;
          border: none;

          .q-btn__wrapper {
            background-color: #dbdfe4;
          }

          &.active {
            .q-btn__wrapper {
              background-color: #4690ff;
            }
          }

          &:hover {
            background-color: #fff;
          }
        }

        &-white {
          &:hover {
            background-color: #fff;
            color: #4690ff;
          }
        }

        &.btn-reset {
          display: none;
        }

        &.btn-del {
          display: block;
          margin: 24px 0px 32px 0px;
        }
      }

      .q-btn {
        .block {
          white-space: nowrap;
        }
      }
    }

    &.group-popup {
      position: fixed !important;
      bottom: 0 !important;
      left: 0 !important;
      top: auto !important;
      width: 100%;
      max-width: 100% !important;
      padding: 8px 16px 16px !important;
      margin: 0 !important;
      min-height: 256px !important;
      box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
      border-radius: 4px 4px 0px 0px;

      .q-item {
        display: inline-block;
        padding: 2px 7px;
        min-height: 0;
        position: relative;
        font-size: 14px;
        line-height: 18px;
        border: 1px solid #a0a9b7;
        border-radius: 4px;
        margin: 0px 17px 16px 0px;

        &:hover {
          background: #fff;
        }

        &__label {
          color: #12284c;
        }

        .q-focus-helper {
          display: none;
        }

        &::before {
          display: none;
        }

        &--active {
          border: 1px solid #f0f5fd;
          color: #12284c;
          background: #f0f5fd !important;
        }
      }

      .group-menu:first-child {
        display: block;

        .group-nav {
          display: flex;
          justify-content: space-between;
          align-items: center;
          margin: -5px 0px 20px;
          padding: 0px 0px 0;

          .group-reset {
            color: #a64541;
            font-weight: 500;
            font-size: 14px;
            line-height: 18px;
          }

          .group-title {
            font-weight: 600;
            font-size: 14px;
            line-height: 18px;
            color: #12284c;
            margin: 0px 45px 0px 0px;
            letter-spacing: 0.1px;
          }

          .group-close {
            cursor: pointer;
            margin: 3px 0px 0px 0px;

            svg {
              path {
                fill: #596982;
              }
            }

            &.active {
              svg {
                path {
                  fill: #12284c;
                }
              }
            }
          }
        }
      }

      .group-btn:last-child {
        display: block;
        position: fixed;
        width: 100%;
        height: 40px;
        bottom: 16px;
        left: 0;
        color: #fff;
        text-align: center;
        padding: 0 16px;

        span {
          display: flex;
          justify-content: center;
          align-items: center;
          min-height: 100%;
          border-radius: 4px;
          background: #dbdfe4;
          font-size: 16px;

          &.active {
            background: #4690ff;
          }
        }
      }
    }

    &.filterOne {
      min-width: 217px !important;
      padding: 0;
      width: calc(100% - 32px);
      transform: translate(-1px, 0px);

      .q-item {
        padding: 11px 24px 10px;
        min-height: 0;
        position: relative;
        background: #fff !important;

        &:hover {
          background: #f3f4f6;
        }

        &__label {
          color: #12284c;
          font-size: 16px;
        }

        .q-focus-helper {
          display: none;
        }

        &--active {
          background: #f3f4f6 !important;
          .q-item__label {
            color: #12284c !important;
          }
        }

        &::before {
          display: none !important;
        }
      }
    }

    &.filterTwo {
      min-width: 0px !important;
      width: calc(100% - 32px);
      transform: translate(-1px, 0px);

      .q-item {
        position: relative;
        font-size: 16px;
        line-height: 20px;
        padding: 11px 24px;

        &::after {
          content: "";
          position: absolute;
          top: 12px;
          right: 16px;
          width: 16px;
          height: 16px;
          background: url("../assets/checkbox-default-16.svg") 0 0 no-repeat;
        }

        &--active {
          &::after {
            background: url("../assets/checkbox-default-16-active.svg") 0 0
              no-repeat;
          }
        }

        &:hover {
          background-color: #fff;
        }
      }
    }

    &.filter-popup {
      position: fixed !important;
      top: 0px !important;
      left: 0px !important;
      min-height: 100% !important;
      margin: 55px 0 0 0 !important;
      padding: 0px !important;
      max-width: 100% !important;
      min-height: 100% !important;
      max-height: 100% !important;
      min-width: 100% !important;
      z-index: 4000;
    }
  }
}
</style>
