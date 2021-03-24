<template>
  <q-page class="mysites-page">
    <div class="confirmation" v-if="mySitesStatus === 'confirmation'">
      <div class="title">Для работы с сайтами и блоками Вам необходимо подтвердить свой электронный адрес, указанный при регистрации.</div>
      <p class="about">
        Пожалуйста, перейдите по ссылке из письма;<br>
        Если письма со ссылкой нет в папке “Входящие”, то проверьте папку “Спам”. Если письмо Вам не пришло, то напишите нам в чат и мы Вам   поможем.
      </p>
    </div>

    <div class="blocked" v-if="mySitesStatus === 'blocked'">
      <div class="title block">Аккаунт заблокирован</div>
    </div>

    <div class="active" v-if="mySitesStatus === 'active'">
      <nav class="nav">
        <q-btn class="btn" :ripple="false" label="Добавить сайт" unelevated no-caps @click="addSite = true" />
        <q-btn class="btn btn-white" label="Обход AdBlock" unelevated no-caps @click="adBlock = true" />
      </nav>

      <div class="row">
        <div class="card sites">
          <q-input class="search" v-model="searchOne" borderless placeholder="Поиск по домену" />

          <q-select
            filled
            v-model="filterSites"
            input-debounce="0"
            label="По дате добавления"
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

          <q-markup-table>
            <thead>
              <tr>
                <th class="text-left">Сайт</th>
                <th class="text-right">Уровень дохода</th>
              </tr>
            </thead>

            <tbody>
              <tr class="active">
                <td>website.website.com</td>
                <td class="status status-hi">
                  <span>Высокий
                    <q-tooltip
                      anchor="top left"
                      self="bottom left"
                      content-class="noarrow"
                      :offset="[0, 8]"
                    >
                      Высокая цена за клик
                    </q-tooltip>
                  </span>
                </td>
              </tr>
              <tr>
                <td>website.website.com</td>
                <td class="status status-low">
                  <span>Низкий
                  <q-tooltip
                      anchor="top left"
                      self="bottom left"
                      content-class="noarrow"
                      :offset="[0, 8]"
                    >
                      Низкая цена за клик
                    </q-tooltip>
                  </span>
                </td>
              </tr>
              <tr>
                <td>website.website.com</td>
                <td class="status status-mid">
                  <span>Средний
                    <q-tooltip
                      anchor="top left"
                      self="bottom left"
                      content-class="noarrow"
                      :offset="[0, 8]"
                    >
                      Средняя цена за клик
                    </q-tooltip>
                  </span>
                </td>
              </tr>
              <tr>
                <td>website.website.com</td>
                <td class="status">На модерации</td>
              </tr>
              <tr>
                <td>website.website.com</td>
                <td class="status status-remoderate">Повторная модерация</td>
              </tr>
              <tr>
                <td>website.website.com</td>
                <td class="status status-blocked">Заблокирован</td>
              </tr>
            </tbody>
          </q-markup-table>
        </div>

        <div class="card blocks">
          <div class="blocks__head">
            <div class="blocks__buttons">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__copy">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M15.5196 9.80005H1.43999C1.19711 9.80005 1 9.99716 1 10.24V22.5597C1 22.803 1.19711 22.9997 1.43999 22.9997H15.5196C15.7629 22.9997 15.9596 22.803 15.9596 22.5597V10.24C15.9596 9.99716 15.7629 9.80005 15.5196 9.80005Z" fill="#DBDFE4"/>
                <path d="M22.5587 1.00024H8.47905C8.23618 1.00024 8.03906 1.19736 8.03906 1.44023V8.48005C8.03906 8.72293 8.23618 8.92004 8.47905 8.92004H16.8388V13.7599C16.8388 14.0032 17.0355 14.1999 17.2788 14.1999H22.5587C22.802 14.1999 22.9987 14.0032 22.9987 13.7599V1.44023C22.9987 1.19736 22.802 1.00024 22.5587 1.00024Z" fill="#DBDFE4"/>
                </svg>
                <q-tooltip
                  anchor="top left"
                  self="bottom left"
                  content-class="noarrow"
                  :offset="[0, 8]"
                >
                  Копировать блок(и)
                </q-tooltip>
              </div>
              <div class="blocks__delete">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M5.14286 20.5556C5.14286 21.9 6.17143 23 7.42857 23H16.5714C17.8286 23 18.8571 21.9 18.8571 20.5556V5.88889H5.14286V20.5556ZM20 2.22222H16L14.8571 1H9.14286L8 2.22222H4V4.66667H20V2.22222Z" fill="#DBDFE4"/>
                </svg>
                <q-tooltip
                  anchor="top left"
                  self="bottom left"
                  content-class="noarrow"
                  :offset="[0, 8]"
                >
                  Удалить блок(и)
                </q-tooltip>
              </div>
            </div>

            <q-input class="search" v-model="searchTwo" borderless placeholder="Поиск по наименованию блока" />

            <q-btn class="btn" :ripple="false" label="Создать блок" unelevated no-caps />
          </div>

          <ul class="blocks__list">
            <li class="blocks__item">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__about">
                <div class="blocks__title">27.07.2020_05:33:28_website.website.com</div>
                <div class="blocks__info">
                  <div class="blocks__id">ID: 973777</div>
                  <div class="blocks__type">Все</div>
                  <div class="blocks__status">Идет тест</div>
                </div>
              </div>
              <div class="blocks__actions">
                <div class="blocks__action">Редактировать</div>
                <div class="blocks__action">Получить код</div>
                <div class="blocks__action">Удалить блок</div>
              </div>
            </li>
            <li class="blocks__item">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__about">
                <div class="blocks__title">27.07.2020_05:33:28_website.website.com</div>
                <div class="blocks__info">
                  <div class="blocks__id">ID: 973777</div>
                  <div class="blocks__type">Все</div>
                  <div class="blocks__status">Идет тест</div>
                </div>
              </div>
              <div class="blocks__actions">
                <div class="blocks__action">Редактировать</div>
                <div class="blocks__action">Получить код</div>
                <div class="blocks__action">Удалить блок</div>
              </div>
            </li>
            <li class="blocks__item">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__about">
                <div class="blocks__title">27.07.2020_05:33:28_website.website.com</div>
                <div class="blocks__info">
                  <div class="blocks__id">ID: 973777</div>
                  <div class="blocks__type">Все</div>
                  <div class="blocks__status">Идет тест</div>
                </div>
              </div>
              <div class="blocks__actions">
                <div class="blocks__action">Редактировать</div>
                <div class="blocks__action">Получить код</div>
                <div class="blocks__action">Удалить блок</div>
              </div>
            </li>
            <li class="blocks__item">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__about">
                <div class="blocks__title">27.07.2020_05:33:28_website.website.com</div>
                <div class="blocks__info">
                  <div class="blocks__id">ID: 973777</div>
                  <div class="blocks__type">Все</div>
                  <div class="blocks__status">Идет тест</div>
                </div>
              </div>
              <div class="blocks__actions">
                <div class="blocks__action">Редактировать</div>
                <div class="blocks__action">Получить код</div>
                <div class="blocks__action">Удалить блок</div>
              </div>
            </li>
            <li class="blocks__item">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__about">
                <div class="blocks__title">27.07.2020_05:33:28_website.website.com</div>
                <div class="blocks__info">
                  <div class="blocks__id">ID: 973777</div>
                  <div class="blocks__type">Все</div>
                  <div class="blocks__status">Идет тест</div>
                </div>
              </div>
              <div class="blocks__actions">
                <div class="blocks__action">Редактировать</div>
                <div class="blocks__action">Получить код</div>
                <div class="blocks__action">Удалить блок</div>
              </div>
            </li>
            <li class="blocks__item">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__about">
                <div class="blocks__title">27.07.2020_05:33:28_website.website.com</div>
                <div class="blocks__info">
                  <div class="blocks__id">ID: 973777</div>
                  <div class="blocks__type">Все</div>
                  <div class="blocks__status">Идет тест</div>
                </div>
              </div>
              <div class="blocks__actions">
                <div class="blocks__action">Редактировать</div>
                <div class="blocks__action">Получить код</div>
                <div class="blocks__action">Удалить блок</div>
              </div>
            </li>
            <li class="blocks__item">
              <div class="blocks__ckeckbox" @click="ckeckbox = !ckeckbox">
                <div v-if="ckeckbox">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M6.98891 8.57784L5.2778 10.2889L10.7778 15.7889L23 3.56673L21.2889 1.85562L10.7778 12.3667L6.98891 8.57784Z" fill="#12284C"/>
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.6805 20.6805H3.31579V3.31579H15.7604V1H3.46006C2.10703 1 1 2.10703 1 3.46007V20.6805C1 22.0336 2.10703 23 3.46006 23H20.6805C22.0335 23 23 22.0336 23 20.6805V10.8403H20.6805V20.6805Z" fill="#12284C"/>
                  </svg>
                </div>
                <div v-else>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8 3.2H3.2V20.8H20.8V3.2ZM3.2 1C1.98497 1 1 1.98497 1 3.2V20.8C1 22.015 1.98497 23 3.2 23H20.8C22.015 23 23 22.015 23 20.8V3.2C23 1.98497 22.015 1 20.8 1H3.2Z" fill="#12284C"/>
                  </svg>
                </div>
              </div>
              <div class="blocks__about">
                <div class="blocks__title">27.07.2020_05:33:28_website.website.com</div>
                <div class="blocks__info">
                  <div class="blocks__id">ID: 973777</div>
                  <div class="blocks__type">Все</div>
                  <div class="blocks__status">Идет тест</div>
                </div>
              </div>
              <div class="blocks__actions">
                <div class="blocks__action">Редактировать</div>
                <div class="blocks__action">Получить код</div>
                <div class="blocks__action">Удалить блок</div>
              </div>
            </li>
          </ul>
        </div>
      </div>

      <q-dialog v-model="addSite">
        <q-card>
          <div class="addsite">
            <div class="title">Добавление сайта</div>

            <q-btn class="close" flat v-close-popup>
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
            </q-btn>

            <div class="label">
              <span>URL-адрес сайта</span>
              <span>Протоколы http:// ; https:// определяются автоматически</span>
            </div>

            <q-input class="url" v-model="searchOne" borderless placeholder="Пример: example.com" />

            <q-select
              filled
              v-model="traffic"
              input-debounce="0"
              label="Выберите тип трафика"
              :options="optionsTwo"
              style="height: 40px"
              dropdown-icon="keyboard_arrow_down"
              popup-content-class="traffic"
              behavior="menu"
              menu-anchor="bottom left"
              menu-self="top left"
              :menu-offset="[1, -10]"
            >
            </q-select>

            <div class="label">
              <span>Ссылка на доступ к статистике сайта</span>
              <span>Инструкция</span>
            </div>

            <q-input class="link" v-model="searchOne" borderless placeholder="Пример: example.com" />

            <div class="info">
              <div class="subtitle">
                Пожалуйста, предоставьте нам гостевой доступ к Вашей статистике для модерации сайта:
              </div>
              <ul class="info__list">
                <li>- Яндекс Метрика (для логина statistics@medicineteaser.ru)</li>
                <li>- Google Analytics (для devtize@gmail.com)</li>
                <li>- liveinternet.ru (гостевой пароль)</li>
              </ul>
            </div>

            <div class="buttons">
              <q-btn class="btn" :ripple="false" label="Отправить" unelevated no-caps />
              <q-btn class="btn btn-grey" :ripple="false" label="Отменить" unelevated no-caps />
            </div>
          </div>
        </q-card>
      </q-dialog>

      <q-dialog v-model="adBlock">
        <q-card>
          <div class="adblock">
            <div class="title">Обход AdBlock (парковка домена)</div>

            <q-btn class="close" flat v-close-popup>
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
            </q-btn>

            <q-expansion-item
              label="Как припарковать домен третьего уровня"
              dropdown-icon="keyboard_arrow_down"
            >
              <q-card>
                <ul class="example__list">
                  <li><a href="#">- пример reg.ru</a></li>
                  <li><a href="#">- пример dns-master.ru</a></li>
                  <li><a href="#">- пример reg.2domains.ru</a></li>
                </ul>

                <p class="text">
                  Если Вы не можете найти информацию о внесении запись «CNAME» к вашему поставщику DNS Вам необходимо обратиться к нему с просьбой прописать новую запись «CNAME» на наш домен <span>flviq0id19.ru</span>
                </p>

                <p class="subtext">
                  Если Ваш сайт работает по HTTPS отставьте заявку на выпуск SSL сертификата, нажав на кнопку «Заказать SSL-сертификат» напротив домена
                </p>
              </q-card>
            </q-expansion-item>

            <q-btn class="btn" :ripple="false" label="Добавить домен" unelevated no-caps @click="addDomain = true" />

            <ul class="sites__list">
              <li>
                <div class="sites__link">https://website.com</div>
                <div class="sites__ssl" @click="ssl = true">Заказать SSL-сертификат</div>
                <div class="sites__del">Удалить</div>
              </li>
              <li>
                <div class="sites__link">https://website.com</div>
                <div class="sites__ssl" @click="ssl = true">Заказать SSL-сертификат</div>
                <div class="sites__del">Удалить</div>
              </li>
            </ul>
          </div>
        </q-card>
      </q-dialog>

      <q-dialog v-model="addDomain">
        <q-card>
          <div class="adddomain">
            <div class="title">Добавление домена для обхода AdBlock</div>

            <q-btn class="close" flat v-close-popup>
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
            </q-btn>

            <div class="label">
              <span>URL-адрес сайта</span>
            </div>

            <q-input class="url" v-model="searchOne" borderless placeholder="Пример: https://example.com" />

            <div class="buttons">
              <q-btn class="btn" :ripple="false" label="Отправить" unelevated no-caps @click="domain = true" />
              <q-btn class="btn btn-grey" :ripple="false" label="Отменить" unelevated no-caps />
            </div>
          </div>
        </q-card>
      </q-dialog>

      <q-dialog v-model="ssl">
        <q-card>
          <div class="ssl">
            <div class="title">Запрос на SSL-сертификат отправлен</div>
            <q-btn class="close" flat v-close-popup>
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
            </q-btn>
          </div>
        </q-card>
      </q-dialog>

      <q-dialog v-model="domain">
        <q-card>
          <div class="domain">
            <div class="title">Домен отправлен на проверку</div>
            <q-btn class="close" flat v-close-popup>
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
            </q-btn>
          </div>
        </q-card>
      </q-dialog>
    </div>

    <div class="mob">
      <a href="#" class="mob__logo"><img src="../assets/logo-mob.png" alt=""/></a>

      <div class="mob__container">
        <img src="../assets/trees.png" alt="">

        <div class="mob__title">
          Страница «Мои сайты» доступна только на десктопной версии 
        </div>
      </div>

      <q-btn class="btn" :ripple="false" label="Перейти" unelevated no-caps />
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      mySitesStatus: 'active', // 'confirmation', 'blocked', 'active'
      searchOne: '',
      searchTwo: '',
      filterSites: null,
      traffic: null,
      optionsOne: ["По дате добавления", "По дате создания", "По дате добавления"],
      optionsTwo: ["Поисковый (органический)", "Платный (покупной)", "Доверенный трафик"],
      ckeckbox: false,
      addSite: false,
      adBlock: false,
      addDomain: false,
      ssl: false,
      domain: false
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

  .mysites-page {
    .title {
      font-weight: 500;
      font-size: 18px;
      line-height: 22px;
      margin: 0px 0px 24px 0px;
      color: #12284C;

      &.block {
        color: #A64541;
      }
    }

    .about {
      font-size: 18px;
      line-height: 32px;
      color: #12284C;
      margin: 0;
    }

    .nav {
      margin: 0px 0px 40px 0px;

      @media (max-width:1650px){
        margin: 0px 0px 32px 0px;
      }
    }

    .btn {
      color: #fff;
      background-color: #4690ff;
      font-size: 18px;
      line-height: 22px;
      height: 40px;
      margin: 0px 24px 0px 0px;

      &:hover {
        background: #629df6;
      }

      .q-btn__wrapper {
        min-height: 0;
        z-index: 1;
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

      @media (max-width:1360px){
        font-weight: 500;
        font-size: 16px;
        line-height: 20px;
      }

      @media (max-width:540px){
        margin: 0px 24px 10px 0px;

        &:last-child {
          margin: 0;
        }
      }
    }

    .row {
      .card {
        box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
        border-radius: 4px;
        padding: 32px 40px 30px;
        height: 100%;

        @media (max-width:1360px){
          padding: 32px 32px 30px;
        }
      }

      .sites {
        flex: 0 1 478px;
        margin: 0px 40px 0px 0px;

        .q-field {
          border: 1px solid #A0A9B7;
          border-radius: 4px;
          height: 40px;
          overflow: hidden;
          margin: 0px 0px 24px 0px;

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

            @media (max-width:1360px){
              font-size: 14px;
              line-height: 17px;
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

            @media (max-width:1360px){
              top: 12px;
              font-size: 14px;
              line-height: 17px;
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

        .q-markup-table {
          margin: 0 -40px;

          @media (max-width:1360px){
            margin: 0 -32px;
          }
        }

        .q-table {
          display: flex;
          flex-direction: column;

          &__card {
            box-shadow: none;
          }

          thead {
            tr {
              width: 100%;
              display: flex;

              th {
                flex: 0 1 50%;
                font-size: 14px;
                line-height: 17px;
                color: #A0A9B7;
                padding: 17px 5px 12px 40px;
                position: relative;

                &.text-left {
                  &::before {
                    content:'';
                    position: absolute;
                    width: 40px;
                    height: 1px;
                    bottom: -1px;
                    left: 0;
                    background-color: #fff;

                    @media (max-width:1360px){
                      width: 32px;
                    }
                  }
                }

                &.text-right {
                  padding: 17px 90px 12px 0px;

                  &::after {
                    content:'';
                    position: absolute;
                    width: 40px;
                    height: 1px;
                    bottom: -1px;
                    right: 0;
                    background-color: #fff;

                    @media (max-width:1360px){
                      width: 32px;
                    }
                  }

                  @media (max-width:1650px){
                    padding: 17px 40px 12px 0px;
                  }

                  @media (max-width:1360px){
                    padding: 17px 37px 12px 0px;
                  }
                }

                @media (max-width:1360px){
                  padding: 17px 5px 12px 32px;
                  font-size: 12px;
                  line-height: 15px;
                }
              }

              @media (max-width:1360px){
                height: 46px;
              }
            }
          }

          tbody {
            display: flex;
            flex-direction: column;

            tr {
              td {
                border-bottom: none;
                font-size: 16px;
                line-height: 20px;
                padding: 23px 0px 15px 40px;
                cursor: pointer;

                &::before {
                  display: none;
                }

                &.status {
                  font-size: 14px !important;
                  line-height: 17px;
                  color: #596982;
                  padding-left: 64px;

                  span {
                    border-radius: 4px;
                    padding: 3px 6px 3px 42px;

                    @media (max-width:1360px){
                      font-size: 12px;
                      line-height: 15px;
                      padding: 4px 6px 4px 42px;
                    }

                    @media (max-width:600px){
                      font-size: 10px;
                    }
                  }

                  &-hi {
                    span {
                      background: #F0F5FD;
                      position: relative;

                      &::before {
                        content:'';
                        position: absolute;
                        width: 28px;
                        height: 8px;
                        top: 8px;
                        left: 6px;
                        background: url('../assets/level-hi.svg') 0 0 no-repeat;
                      }
                    }
                  }

                  &-mid {
                    span {
                      background: #F7F3C5;
                      position: relative;

                      &::before {
                        content:'';
                        position: absolute;
                        width: 28px;
                        height: 8px;
                        top: 8px;
                        left: 6px;
                        background: url('../assets/level-mid.svg') 0 0 no-repeat;
                      }
                    }
                  }

                  &-low {
                    span {
                      background: #F7C9CB;
                      position: relative;

                      &::before {
                        content:'';
                        position: absolute;
                        width: 28px;
                        height: 8px;
                        top: 8px;
                        left: 6px;
                        background: url('../assets/level-low.svg') 0 0 no-repeat;
                      }
                    }
                  }

                  &-remoderate {
                    color: #4690FF;
                  }

                  &-blocked {
                    color: #A64541;
                  }

                  @media (max-width:1650px){
                    padding-left: 40px;
                  }

                  @media (max-width:1170px){
                    text-align: right;
                  }

                  @media (max-width:600px){
                    padding-left: 5px;
                    font-size: 12px !important;
                  }
                }

                @media (max-width:1360px){
                  font-size: 14px;
                  line-height: 17px;
                  padding: 23px 0px 17px 32px;
                }

                @media (max-width:1170px){
                  flex: 0 1 50%;
                  height: auto;
                  padding: 23px 32px 17px 32px;
                }

                @media (max-width:600px){
                  font-size: 12px;
                }
              }

              &.active{
                position: relative;

                &::after {
                  content:'';
                  position: absolute;
                  width: 2px;
                  height: 48px;
                  top: 8px;
                  right: 0px;
                  background: #4690FF;
                }
              }

              @media (max-width:1170px){
                display: flex;
              }
            }

            @media (max-width:1360px){
              margin: 5px 0px 0px 0px;
            }
          }

          &--no-wrap th, &--no-wrap td {
            white-space: nowrap;

            @media (max-width:1650px){
              white-space: normal !important;
            }
          }
        }

        @media (max-width:1650px){
          flex: 0 1 404px;
        }

        @media (max-width:1360px){
          flex: 0 1 355px;
          margin: 0px 32px 0px 0px;
        }

        @media (max-width:1170px){
          flex: 1 1 100%;
          margin: 0px 0px 32px 0px;
        }
      }

      .blocks {
        flex: 1 1 auto;
        padding: 32px 40px 40px;

        &__head {
          display: flex;
          justify-content: space-between;
          padding: 0px 0px 23px 0px;
          border-bottom: 1px solid #F3F4F6;

          .btn {
            margin: 0;
          }

          .q-field {
            border: 1px solid #A0A9B7;
            border-radius: 4px;
            height: 40px;
            overflow: hidden;
            margin: 0px 0px 24px 0px;
            min-width: 345px;

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

              @media (max-width:1250px){
                font-size: 14px;
                line-height: 17px;
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
            }

            @media (max-width:1650px){
              min-width: 292px;
            }

            @media (max-width:1250px){
              min-width: 253px;
              max-width: 253px;
            }

            @media (max-width:800px){
              max-width: 100%;
            }
          }

          .search {
            margin: 0px 48px 0px auto;
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

                @media (max-width:1250px){
                  font-size: 14px;
                  line-height: 17px;
                  padding: 9px 16px 7px 50px;
                }

                @media (max-width:600px){
                  font-size: 12px;
                }
              }
            }

            @media (max-width:1800px){
              margin: 0px 32px 0px auto;
            }

            @media (max-width:1250px){
              margin: 0px 24px 0px auto;
            }

            @media (max-width:800px){
              margin: 0px 0px 16px 0px;
            }
          }

          @media (max-width:800px){
            display: block;
          }
        }

        &__buttons {
          display: flex;
        }

        &__ckeckbox, &__copy, &__delete {
          margin: 8px 24px 0px 0px;
          cursor: pointer;

          @media (max-width:1250px){
            margin: 8px 16px 0px 0px;
          }

          @media (max-width:800px){
            margin: 0px 16px 15px 0px;
          }
        }

        &__list {
          list-style: none;
          margin: 0;
          padding: 0;
        }

        &__row {
          display: flex;
        }

        &__info {
          display: flex;
          font-weight: 500;
          font-size: 14px;
          line-height: 17px;

          @media (max-width:1360px){
            font-size: 12px;
            line-height: 15px;
          }
        }

        &__id, &__type, &__status {
          margin: 0px 24px 0px 0px;
        }

        &__status {
          color: #95BD5A;
        }

        &__item {
          display: flex;
          justify-content: space-between;
          margin: 32px 0px 39px;

          .blocks__ckeckbox {
            margin: 0 32px 0 0;

            @media (max-width:1650px){
              align-self: flex-start;
              margin: 25px 32px 0px 0px;
            }

            @media (max-width:1250px){
              margin: 23px 32px 0px 0px;
            }

            @media (max-width:800px){
              margin: 23px 32px 10px 0px;
            }
          }

          &:last-child {
            margin: 32px 0px 0px;
          }

          @media (max-width:1650px){
            &:first-child {
              margin: 32px 0px 23px;
            }

            align-items: center;
            margin: 0px 0px 21px;

            &:last-child {
              margin: 0px;
            }
          }

          @media (max-width:800px){
            display: block;

            &:first-child {
              margin: 32px 0;
            }

            margin: 32px 0px;
          }
        }

        &__about {
          @media (max-width:1650px){
            margin: 0px 0px 16px 0px;
          }
        }

        &__actions {
          display: flex;
          align-self: center;
          margin: 0px 37px 0px auto;

          @media (max-width:1800px){
            display: block;
            margin: 0px 0px 0px auto;
          }
        }

        &__title {
          font-size: 16px;
          line-height: 20px;
          margin: 1px 0px 12px 0px;

          @media (max-width:1360px){
            font-size: 14px;
            line-height: 17px;
          }

          @media (max-width:600px){
            font-size: 12px;
          }
        }

        &__action {
          color: #4690FF;
          font-weight: 500;
          font-size: 16px;
          line-height: 20px;
          margin: 0px 0px 0px 25px;
          cursor: pointer;

          &:hover{
            color: #629DF6;
          }

          @media (max-width:1800px){
            display: block;
            margin: 2px 0px 18px 25px;
          }

          @media (max-width:1360px){
            font-size: 14px;
            line-height: 17px;
          }

          @media (max-width:800px){
            margin: 2px 0px 10px 0px;
          }
        }

        @media (max-width:1360px){
          padding: 32px;
        }
      }
    }

    .mob {
      display: none;
    }
  }

  .q-menu {
    &.filterSites {
      width: 396px;

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

      @media (max-width:1650px){
        width: 324px;
      }

      @media (max-width:1360px){
        width: 289px;
      }

      @media (max-width:1170px){
        width: calc(100% - 240px);
      }
    }

    &.traffic {
      width: 497px;

      .q-item {
        min-height: 40px;

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

      @media (max-width:630px){
        width: calc(100% - 130px);
      }
    }
  }

  .q-dialog {
    &__backdrop {
      background: #12284c;
      opacity: 0.2;
    }

    &__inner--minimized > div {
      max-width: 639px;
    }

    &__inner > div {
      box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
    }

    .addsite {
      padding: 40px;
      min-width: 100%;
      min-height: 100%;
      max-width: 577px;
      max-height: 548px;

      .title {
        font-weight: 500;
        font-size: 18px;
        line-height: 22px;
        color: #12284C;
        margin: 0px 0px 33px 0px;
      }

      .close {
        position: absolute;
        width: 24px;
        height: 24px;
        top: 33px;
        right: 40px;

        .q-btn__wrapper {
          padding: 0;
          margin: 0;
        }

        .q-focus-helper {
          display: none;
        }

        &:hover{
          svg {
            path {
              transition: all 0.3s;
              fill: #12284C;
            }
          }
        }      }

      .label {
        font-size: 12px;
        line-height: 15px;
        color: #12284C;
        display: flex;
        justify-content: space-between;
        margin: 0px 0px 8px 0px;

        span {
          &:last-child {
            color: #A0A9B7;
          }
        }
      }

      .q-field {
        border: 1px solid #A0A9B7;
        border-radius: 4px;
        height: 40px;
        overflow: hidden;
        margin: 0px 0px 24px 0px;

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

      .url {
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

      .link {
        margin: 0px 0px 16px 0px;
      }

      .info {
        font-size: 14px;
        line-height: 18px;

        .subtitle {
          color: #12284C;
          padding: 0px 0px 0px 24px;
          position: relative;
          margin: 0px 0px 8px 0px;

          &::before {
            content:'';
            position: absolute;
            width: 16px;
            height: 16px;
            top: 0;
            left: 0;
            background: url('../assets/attention.svg') 0 0 no-repeat;
          }
        }

        &__list {
          list-style: none;
          padding: 0 0 0 24px;
          margin: 0 0 32px 0;

          li {
            font-size: 14px;
            line-height: 22px;
            color: #596982;
          }
        }
      }

      .buttons {
        display: flex;
        justify-content: flex-end;

        .btn {
          color: #fff;
          background-color: #4690ff;
          font-size: 18px;
          line-height: 22px;
          height: 40px;

          & + .btn {
            margin: 0px 0px 0px 24px;
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

      @media (max-width:600px){
        max-height: 100%;
      }
    }

    .adblock {
      padding: 40px;
      min-width: 100%;
      min-height: 100%;
      max-width: 639px;
      min-width: 576px;

      .title {
        font-weight: 500;
        font-size: 18px;
        line-height: 22px;
        color: #12284C;
        margin: 0px 0px 30px 0px;
      }

      .close {
        position: absolute;
        width: 24px;
        height: 24px;
        top: 33px;
        right: 40px;

        .q-btn__wrapper {
          padding: 0;
          margin: 0;
        }

        .q-focus-helper {
          display: none;
        }

        &:hover{
          svg {
            path {
              transition: all 0.3s;
              fill: #12284C;
            }
          }
        }
      }

      .q-expansion-item {
        .q-focus-helper {
          display: none;
        }

        .q-item {
          padding: 0;
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
          color: #4690ff;
          font-size: 34px;
          margin: 0px -5px 0px 0px;
        }

      }

      .btn {
        color: #fff;
        background-color: #4690ff;
        font-size: 18px;
        line-height: 22px;
        height: 40px;
        margin: 18px 0px 0px 0px;

        & + .btn {
          margin: 0px 0px 0px 24px;
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

      .example__list {
        padding: 0;
        margin: 6px 0 8px 0;
        list-style: none;
        font-weight: 500;
        font-size: 14px;
        line-height: 20px;
        color: #12284C;

        li {
          a {
            text-decoration: none;
            color: #12284C;
          }
        }
      }

      .text {
        font-size: 14px;
        line-height: 24px;
        color: #12284C;
        padding: 0;
        margin: 0 0 8px 0;

        span {
          font-weight: 500;
          font-size: 14px;
          line-height: 24px;
        }
      }

      .subtext {
        font-size: 14px;
        line-height: 24px;
        color: #596982;
        padding: 0;
        margin: 0 0 6px 0;
      }

      .sites {
        &__list {
          padding: 0;
          margin: 41px 0px 0px 0px;
          list-style: none;

          li {
            font-size: 18px;
            line-height: 22px;
            display: flex;
            justify-content: space-between;
            flex-wrap: nowrap;
            min-width: 559px;

            & + li {
              margin: 42px 0px 9px 0px;
            }

            @media (max-width:700px){
              display: block;
            }
          }
        }

        &__link {
          color: #12284C;
          cursor: pointer;

          @media (max-width:700px){
            margin: 0px 0px 10px 0px;
          }
        }

        &__ssl {
          color: #596982;
          letter-spacing: 0.2px;
          letter-spacing: 0.2102px;
          margin: 0 24px 0 40px;
          cursor: pointer;

          @media (max-width:700px){
            margin: 0px 0px 10px 0px;
          }
        }

        &__del {
          color: #B36F6C;
          cursor: pointer;
        }
      }

      @media (max-width:700px){
        min-width: 0;
        overflow: hidden;
      }
    }

    .adddomain {
      padding: 40px;
      min-height: 100%;
      min-width: 595px;
      max-width: 595px;
      max-height: 548px;

      .title {
        font-weight: 500;
        font-size: 18px;
        line-height: 22px;
        color: #12284C;
        margin: 0px 0px 33px 0px;

        @media (max-width:645px){
          margin: 0px 30px 33px 0px;
        }
      }

      .close {
        position: absolute;
        width: 24px;
        height: 24px;
        top: 33px;
        right: 40px;

        .q-btn__wrapper {
          padding: 0;
          margin: 0;
        }

        .q-focus-helper {
          display: none;
        }

        &:hover{
          svg {
            path {
              transition: all 0.3s;
              fill: #12284C;
            }
          }
        }      }

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
        }
      }

      .url {
        .q-field {
          &__native {
            padding: 9px 16px 7px 16px;
            font-size: 16px;
            line-height: 20px;
            letter-spacing: -0.1px;
          }
        }
      }

      .link {
        margin: 0px 0px 16px 0px;
      }

      .buttons {
        display: flex;
        justify-content: flex-end;

        .btn {
          color: #fff;
          background-color: #4690ff;
          font-size: 18px;
          line-height: 22px;
          height: 40px;

          & + .btn {
            margin: 0px 0px 0px 24px;
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

      @media (max-width:645px){
        max-width: 100%;
        min-width: 100%;
        overflow: hidden;
      }
    }

    .ssl {
      padding: 40px;
      min-width: 100%;
      min-height: 100%;
      max-width: 440px;
      min-width: 440px;

      .title {
        font-weight: 500;
        font-size: 18px;
        line-height: 22px;
        color: #95BD5A;
        margin: 48px 0px 0px 0px;
      }

      .close {
        position: absolute;
        width: 24px;
        height: 24px;
        top: 33px;
        right: 40px;

        .q-btn__wrapper {
          padding: 0;
          margin: 0;
        }

        .q-focus-helper {
          display: none;
        }

        &:hover{
          svg {
            path {
              transition: all 0.3s;
              fill: #12284C;
            }
          }
        }
      }
    }

    .domain {
      padding: 40px;
      min-width: 100%;
      min-height: 100%;
      max-width: 374px;
      min-width: 374px;

      .title {
        font-weight: 500;
        font-size: 18px;
        line-height: 22px;
        color: #95BD5A;
        margin: 48px 0px 0px 0px;
      }

      .close {
        position: absolute;
        width: 24px;
        height: 24px;
        top: 33px;
        right: 40px;

        .q-btn__wrapper {
          padding: 0;
          margin: 0;
        }

        .q-focus-helper {
          display: none;
        }

        &:hover{
          svg {
            path {
              transition: all 0.3s;
              fill: #12284C;
            }
          }
        }
      }
    }
  }

  // Mobile
  @media (max-width:500px){
    .mysites-page {
      .confirmation, .blocked, .active {
        display: none;
      }

      .mob {      
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        display: flex;
        flex-direction: column;
        justify-content:center;
        align-items: center;
        padding: 16px;

        &__logo {
          position: absolute;
          width: 65px;
          height: 21px;
          top: 16px;
          left: 16px;
        }

        &__container {
          max-width: 328px;        

          img {
            max-width: 100%;
          }        
        }

        &__title {
          margin: 56px 0px 24px 0px;
          text-align: center;
          font-weight: 500;
          font-size: 16px;
          line-height: 24px;
        }

        .btn {
          width: 100%;
        }
      }
    }

  }
</style>
