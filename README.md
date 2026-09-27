# E-home — исправленная миграция GitHub Pages

## Что исправлено

- Второй аргумент `YaAuthSuggest.init()` теперь равен только `https://lantigan-dot.github.io`.
- `YaSendSuggestToken()` получает только origin, без пути `/E_home/`.
- Callback запускается после полной загрузки SDK.
- Добавлены проверки HTTPS, origin, callback и загрузки SDK.
- Добавлены favicon и PWA-иконки, чтобы убрать 404 для иконки.
- Использован Client ID, который сейчас опубликован в вашем `config.js`.

## Установка

1. Удалите старые файлы в корне репозитория `E_home` или замените их файлами из архива.
2. Загрузите все файлы из архива в корень ветки `main`.
3. Дождитесь завершения GitHub Pages deployment.
4. Проверьте:
   - https://lantigan-dot.github.io/E_home/
   - https://lantigan-dot.github.io/E_home/config.js
   - https://lantigan-dot.github.io/E_home/yandex-token.html
5. В Яндекс OAuth значение Redirect URI должно быть ровно:
   `https://lantigan-dot.github.io/E_home/yandex-token.html`
6. Откройте сайт в приватной вкладке или очистите кэш старой версии.

## Безопасность

`Client ID` допустимо использовать во frontend. `Client secret` нельзя добавлять в эти файлы, GitHub или браузерный код.

## Примечание

Полный OAuth-вход требует пользовательской сессии и подтверждения на стороне Яндекса; локальные тесты проверяют структуру, синтаксис, URL, origin и доступность Client ID.
