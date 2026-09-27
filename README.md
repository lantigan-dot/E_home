# Публикация на GitHub Pages для ЭНЕРГО + Яндекс ID

Да, **GitHub Pages подходит** для публикации этой версии, потому что GitHub Pages поддерживает HTTPS для `github.io`-сайтов и для корректно настроенных custom domain, а HTTPS можно принудительно включить в настройках Pages [web:112][web:115]. Для Яндекс OAuth это важно, так как redirect URI должен быть HTTPS-адресом и должен точно совпадать с зарегистрированным адресом возврата [web:79][web:124].

## Вариант 1 — самый простой: `github.io`

Если ваш GitHub-логин `alexey`, а репозиторий называется `energo`, итоговый адрес обычно будет:

`https://alexey.github.io/energo/`

Тогда callback-страница для Яндекса должна быть:

`https://alexey.github.io/energo/yandex-token.html`

## Что загрузить в репозиторий

Положите в корень репозитория эти файлы:

- `index.html`
- `yandex-token.html`
- `config.js`
- `.nojekyll`

## Шаги публикации

1. Создайте новый публичный репозиторий на GitHub.
2. Загрузите в него файлы из этого архива.
3. В `Settings` → `Pages` выберите публикацию из ветки `main` и корня `/root`.
4. Дождитесь появления адреса вида `https://<user>.github.io/<repo>/`.
5. Включите `Enforce HTTPS`, когда опция станет доступна.
6. В кабинете Яндекс OAuth создайте приложение типа **Web services**.
7. В `Redirect URI` укажите точный адрес callback-страницы GitHub Pages.
8. Добавьте права `iot:view` и `iot:control`.
9. Скопируйте выданный `Client ID`.
10. Откройте `config.js` и замените значения на реальные.
11. Закоммитьте обновлённый `config.js` в репозиторий.
12. После обновления сайта нажмите кнопку входа через Яндекс ID.

## Как заполнить `config.js`

Для адреса `https://alexey.github.io/energo/` файл должен выглядеть так:

```js
window.ENERGO_CONFIG = Object.freeze({
  yandexClientId: 'ВАШ_CLIENT_ID',
  appOrigin: 'https://alexey.github.io',
  appBasePath: '/energo/',
  redirectUri: 'https://alexey.github.io/energo/yandex-token.html',
  apiBase: 'https://api.iot.yandex.net'
});
```

## Важная особенность GitHub Pages

У GitHub Pages для project site есть base path вида `/<repo>/`, поэтому callback и все внутренние ссылки должны учитывать путь репозитория, а не только origin. HTTPS для Pages поддерживается GitHub официально, а для custom domain HTTPS также поддерживается после корректной настройки DNS и сертификата [web:111][web:116].

## Если будет custom domain

Например, если вы позже подключите `https://energy.example.ru`, тогда:

- `appOrigin = 'https://energy.example.ru'`
- `appBasePath = '/'`
- `redirectUri = 'https://energy.example.ru/yandex-token.html'`

GitHub Pages создаёт или использует `CNAME` для custom domain, а HTTPS можно включить после выпуска сертификата [web:111][web:116].

## Частые ошибки

- В Яндекс OAuth указан `https://alexey.github.io/yandex-token.html`, а сайт реально открыт как `https://alexey.github.io/energo/...`.
- В `redirect_uri` отличается хотя бы один символ или слэш.
- Не включён `Enforce HTTPS`.
- В `config.js` указан не тот `Client ID`.
- Сайт ещё не успел перепубликоваться в Pages.

Redirect URI у Яндекса должен совпадать **буквально**, иначе параметр игнорируется или возникает ошибка [web:124].
