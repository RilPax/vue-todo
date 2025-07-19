# Todo — приложение для управления задачами

Простой и быстрый to-do список, созданный с использованием Vue 3 и TypeScript.

---

## Технологии

- [Vite](https://vitejs.dev/) — сборщик
- [Vue 3](https://vuejs.org/) — фреймворк
- [TypeScript](https://www.typescriptlang.org/) — типизация
- [Prettier](https://prettier.io/) — форматирование кода
- [ESLint](https://eslint.org/) — линтинг
- [Lucide](https://lucide.dev/) — иконки SVG

---

## Как запустить проект

```bash
# Установить зависимости
npm install
# или
yarn install

# Запустить в режиме разработки
npm run dev

# Собрать production-билд
npm run build

# Предпросмотр production-билда
npm run preview

```

## Структура проекта

- src/components/todo-item.vue — компонент одной задачи

- src/components/todo-list.vue — список всех задач

- src/App.vue — корневой компонент приложения

- src/main.ts — точка входа в приложение

## Функциональность

Пользователь может:

- Добавлять задачи

- Удалять задачи

- Отмечать задачи как выполненные

- Все изменения сохраняются в localStorage