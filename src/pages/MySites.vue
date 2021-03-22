<template>
  <q-page class="mysites-page">
    <div v-if="mySitesStatus === 'confirmation'">
      <div class="title">Для работы с сайтами и блоками Вам необходимо подтвердить свой электронный адрес, указанный при регистрации.</div>
      <p class="about">
        Пожалуйста, перейдите по ссылке из письма;<br>
        Если письма со ссылкой нет в папке “Входящие”, то проверьте папку “Спам”. Если письмо Вам не пришло, то напишите нам в чат и мы Вам   поможем.
      </p>
    </div>

    <div v-if="mySitesStatus === 'blocked'">
      <div class="title block">Аккаунт заблокирован</div>
    </div>

    <div v-if="mySitesStatus === 'active'">
      <nav class="nav">
        <q-btn class="btn" :ripple="false" label="Добавить сайт" unelevated no-caps @click="addSite = true, lockPage = !lockPage" />
        <q-btn class="btn btn-white" label="Обход AdBlock" unelevated no-caps />
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

            <div>
              <span>URL-адрес сайта</span>
              <span>Протоколы http:// ; https:// определяются автоматически</span>
              <q-input class="url" v-model="searchOne" borderless placeholder="Пример: example.com" />
            </div>

            <q-select
              filled
              v-model="filterSites"
              input-debounce="0"
              label="Выберите тип трафика"
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

            <div>
              <span>URL-адрес сайта</span>
              <span>Протоколы http:// ; https:// определяются автоматически</span>
              <q-input class="url" v-model="searchOne" borderless placeholder="Пример: example.com" />
            </div>

            <div class="info">
              <div class="subtitle">
                Пожалуйста, предоставьте нам гостевой доступ к Вашей статистике для модерации сайта:
              </div>
              <ul class="imfo__list">
                <li>- Яндекс Метрика (для логина statistics@medicineteaser.ru)</li>
                <li>- Google Analytics (для devtize@gmail.com)</li>
                <li>- liveinternet.ru (гостевой пароль)</li>
              </ul>
            </div>

            <div class="buttons">
              <q-btn class="btn" :ripple="false" label="Отправить" unelevated no-caps />
              <q-btn class="btn" :ripple="false" label="Отменить" unelevated no-caps />
            </div>
          </div>
        </q-card>
      </q-dialog>
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
      optionsOne: ["По дате добавления", "По дате создания", "По дате добавления"],
      ckeckbox: false,
      addSite: false,
      lockPage: false
    }
  }
}
</script>


<style lang="scss">
  .q-page {
    padding: 40px 40px 0;
  }

  .mysites-page {
    &.lock {

    }

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
    }

    .row {
      .card {
        box-shadow: 0px 0px 24px rgba(18, 40, 76, 0.08);
        border-radius: 4px;
        padding: 32px 40px 30px;
        height: 100%;
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
            }
          }
        }

        .q-markup-table {
          margin: 0 -40px;
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
                  }
                }
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
            }
          }
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
              }
            }
          }
        }

        &__buttons {
          display: flex;
        }

        &__ckeckbox, &__copy, &__delete {
          margin: 8px 24px 0px 0px;
          cursor: pointer;
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
          }

          &:last-child {
            margin: 32px 0px 0px;
          }
        }

        &__actions {
          display: flex;
          align-self: center;
          margin: 0px 37px 0px auto;
        }

        &__title {
          font-size: 16px;
          line-height: 20px;
          margin: 1px 0px 12px 0px;
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
        }
      }
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
    }
  }

  .q-dialog {
    &__backdrop {
      background: #12284c;
      opacity: 0.2;
    }

    .addsite {
      padding: 40px !important;
      min-width: 100%;
      min-height: 100%;
      max-width: 577px;
      max-height: 548px;

      .title {
        font-weight: 500;
        font-size: 18px;
        line-height: 22px;
        color: #12284C;
      }

      .close {
        .q-btn__wrapper {
          padding: 0;
          margin: 0;
        }

        .q-focus-helper {
          display: none;
        }
      }
    }
  }
</style>
