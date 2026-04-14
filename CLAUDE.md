# SmartRanking Landings — Правила работы

## Что это

Репозиторий HTML-лендингов и отчётов, которые публикуются на smartranking.ru/ru/offers/. Каждая папка — отдельная страница.

## Структура

```
smartranking-landings/
├── bigtech100-offer/        → /ru/offers/bigtech100-offer/
│   └── index.html, logo.svg, top10-chart.jpg, print.html, PDF
├── edtechs-partnership/     → /ru/offers/edtechs-partnership/
│   └── index.html, logo.svg, edtech-logo.png
├── smartranking-partnership/ → /ru/offers/smartranking-partnership/
│   └── index.html, logo.svg
├── smart500-partnership/    → /ru/offers/smart500-partnership/
│   └── index.html, logo.svg, smart500.webp
├── online-fitness-report/   → /ru/offers/online-fitness-report/
│   └── index.html, images/
├── logos/                   → общие логотипы партнёров
└── CLAUDE.md                → этот файл
```

## Деплой

**Автоматический.** Push в `main` → через ~1 минуту файлы на проде (smartranking.ru).

Cron на сервере smartranking.ru каждую минуту делает `git pull`.

## Как редактировать

### Текст на странице
1. Открой нужный `index.html`
2. Найди текст, который нужно изменить
3. Отредактируй
4. `git add`, `git commit`, `git push origin main`
5. Через минуту изменения на сайте

### Новая страница
1. Создай папку: `new-page-name/`
2. Создай `index.html` внутри
3. Изображения клади в ту же папку или в `images/`
4. Push → автодеплой

## Правила редактирования

### КРИТИЧНО
- **НЕ удалять** Яндекс.Метрику (counter 84884446) из страниц
- **НЕ удалять** `<meta name="robots" content="noindex, nofollow"/>` — страницы не должны индексироваться
- **НЕ менять** структуру HTML без согласования — только текст и данные
- **НЕ коммитить** пароли, токены, ключи

### Стилистика
- Все страницы используют Tailwind CSS через CDN
- Шрифты: Manrope (заголовки), Inter (текст)
- Основные цвета: primary #003d9b, background #faf8ff, on-background #131b2e
- Иконки: Material Symbols Outlined
- Максимальная ширина контента: 960px

### Коммиты
Формат: `<действие> <что> [контекст]`
- "Update fitness report: fix typo in section 2.1"
- "Add new partnership offer page"
- "Fix broken image path in bigtech100"

### Изображения
- Оптимизировать перед коммитом (не больше 500KB на картинку)
- Форматы: .jpg для фото, .png для графиков, .svg для логотипов, .webp где возможно
- Класть рядом с index.html или в `images/` подпапку

## Git

```bash
cd /home/node/.openclaw/workspace/smartranking-landings
git pull origin main          # перед редактированием
# ... редактируешь файлы ...
git add -A
git commit -m "описание"
git push origin main          # деплой через ~1 мин
```

## Проверка

После push можно проверить:
```
curl -s -o /dev/null -w "%{http_code}" https://smartranking.ru/ru/offers/ПАПКА/
```
Должен вернуть 200.
