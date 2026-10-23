# DMWorks Design

Единый источник темы и компонентов для всех продуктов DMWorks: Signum, Creator Studio, DMWorks Net, Speedtest.

## Как устроено

```
tokens/tokens.json            цвета (тёмная, светлая, рабочая), отступы, скругления, шрифты
components/core/*.css         общие компоненты: dm-btn, dm-row, dm-chip…
components/apps/<app>/*.css   компоненты одного продукта: dm-<app>-…
build.mjs                     собирает dist/
dist/tokens.css               только токены
dist/dmworks.css              токены + общие компоненты
dist/apps/<app>.css           компоненты продукта
```

Правки только в `tokens/` и `components/`, потом `node build.mjs`. `dist/` не трогать руками.

## Подключение

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/DenisMaydenkov/dmworks-design@v1/dist/dmworks.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/DenisMaydenkov/dmworks-design@v1/dist/apps/speedtest.css">
```

Тема — `data-theme="dark|light|pro"` на `<html>`. Жёлтые предупреждения — `data-warning="yellow"`.

`@v1` — версия. Совместимые правки (новые компоненты, подстройка цветов) выходят как `v1.x`, и все продукты на `@v1` получают их сами. Ломающие (переименование токена, удаление компонента) — `v2`, продукт переходит, когда готов.

## Как расширять

1. **Компонент для одного продукта** — файл в `components/apps/<app>/`, классы `dm-<app>-…`, только токены, без своих цветов и отступов.
2. **Понадобился второму продукту** — перенести файл в `components/core/`, убрать `<app>-` из имени, старое имя оставить алиасом до следующей мажорной версии.
3. **Новый токен** — в `tokens/tokens.json` с полем `usage`; значение для каждой темы.
