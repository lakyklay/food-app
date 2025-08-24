# 🍕 Food App - Конструктор мобильных приложений для заказа еды

Модульная платформа для создания мобильных приложений доставки еды с конструктором блюд, кастомизацией ингредиентов, корзиной, оформлением заказа и реферально-бонусной системой. Архитектура "как конструктор" - переиспользуемые модули для разных брендов и сетей.

## 🚀 Быстрый старт

### Вариант 1: Запуск через npm скрипты (рекомендуется)

```bash
# Установка всех зависимостей
npm run install:all

# Запуск backend и mobile одновременно
npm run dev
```

### Вариант 2: Запуск через Docker

```bash
# Запуск всех сервисов (backend + PostgreSQL + Redis)
docker-compose up -d

# Запуск только mobile
cd mobile && npm start
```

### Вариант 3: Ручной запуск

```bash
# Terminal 1: Backend
cd backend && go run main.go

# Terminal 2: Mobile
cd mobile && npm start
```

## 📱 Архитектура проекта

- **Backend**: Go + Gin (REST API)
- **Mobile**: React Native + Expo + TypeScript
- **База данных**: PostgreSQL (планируется)
- **Кеш**: Redis (планируется)

## 📁 Структура проекта

```
food-app/
├── backend/          # Go API сервер
│   ├── main.go      # Основной файл сервера
│   ├── go.mod       # Go зависимости
│   └── Dockerfile   # Docker конфигурация
├── mobile/           # React Native приложение
│   ├── src/
│   │   ├── api/     # API клиент
│   │   └── screens/ # Экраны приложения
│   ├── App.tsx      # Главный компонент
│   └── package.json # Node.js зависимости
├── docker-compose.yml # Docker Compose конфигурация
├── package.json     # Корневые скрипты
└── spec.md          # Техническое задание
```

## ⚙️ Требования

### Backend
- Go 1.24.2+
- PostgreSQL (для продакшена)

### Mobile
- Node.js 18+
- Expo CLI
- iOS Simulator / Android Emulator

### Docker (опционально)
- Docker Desktop
- Docker Compose

## 🔧 Установка и настройка

### 1. Клонирование и установка

```bash
git clone <repository-url>
cd food-app

# Установка всех зависимостей
npm run install:all
```

### 2. Настройка переменных окружения

Создайте файл `.env` в корне проекта:

```env
# Backend
BACKEND_PORT=8080
DATABASE_URL=postgresql://foodapp:foodapp123@localhost:5432/foodapp
REDIS_URL=redis://localhost:6379

# Mobile
EXPO_PUBLIC_API_BASE=http://localhost:8080/api
```

### 3. Запуск в режиме разработки

```bash
# Запуск backend и mobile одновременно
npm run dev
```

После запуска:
- Backend будет доступен на `http://localhost:8080`
- Expo DevTools откроется в браузере
- Нажмите `i` для iOS Simulator
- Нажмите `a` для Android Emulator
- Отсканируйте QR код для физического устройства

## 📡 API Endpoints

### Аутентификация
- `POST /api/auth/request-otp` - Запрос OTP
- `POST /api/auth/verify-otp` - Подтверждение OTP
- `POST /api/auth/refresh` - Обновление токена

### Каталог
- `GET /api/catalog` - Получение категорий
- `GET /api/products` - Список продуктов
- `GET /api/products/:id` - Детали продукта

### Корзина
- `POST /api/cart` - Создание корзины
- `POST /api/cart/items` - Добавление товара
- `PATCH /api/cart/items/:id` - Изменение товара
- `POST /api/cart/apply-promo` - Применение промокода
- `POST /api/cart/apply-bonuses` - Применение бонусов
- `GET /api/cart/totals` - Расчет итогов

### Оформление заказа
- `POST /api/checkout/quote` - Получение квоты
- `POST /api/checkout/place` - Размещение заказа
- `GET /api/orders/:id` - Статус заказа

### Профиль
- `GET /api/me` - Профиль пользователя
- `GET /api/me/wallet` - Баланс кошелька

## ✅ Функциональность

### ✅ Реализовано (MVP)
- [x] Каталог продуктов с типизацией
- [x] Детальная страница товара с вариантами и аллергенами
- [x] Корзина с детальным расчетом
- [x] Оформление заказа с квотой доставки
- [x] Отслеживание статуса заказа в реальном времени
- [x] Безопасная навигация с TypeScript
- [x] Обработка ошибок и состояний загрузки
- [x] Современный UI с SafeAreaView

### 🚧 В разработке
- [ ] Аутентификация пользователей
- [ ] Конструктор блюд (модификаторы)
- [ ] Система бонусов и рефералов
- [ ] Stories и акции
- [ ] Админ-панель
- [ ] Push-уведомления
- [ ] Интеграция с платежными системами
- [ ] База данных PostgreSQL
- [ ] Кеширование Redis

## 🛠️ Разработка

### Доступные команды

```bash
# Установка зависимостей
npm run install:all

# Запуск в режиме разработки
npm run dev

# Запуск только backend
npm run start:backend

# Запуск только mobile
npm run start:mobile

# Сборка backend
npm run build:backend

# Тестирование
npm run test:backend
npm run test:mobile

# Очистка
npm run clean
```

### Docker команды

```bash
# Запуск всех сервисов
docker-compose up -d

# Просмотр логов
docker-compose logs -f

# Остановка сервисов
docker-compose down

# Пересборка
docker-compose up --build
```

## 🧪 Тестирование

### Backend
```bash
cd backend
go test ./...
```

### Mobile
```bash
cd mobile
npx tsc --noEmit
```

## 📦 Деплой

### Backend
```bash
# Локальная сборка
cd backend
go build -o foodapp-backend .

# Docker сборка
docker build -t foodapp-backend ./backend
```

### Mobile
```bash
cd mobile
expo build:android  # для Android
expo build:ios      # для iOS
```

## 🔍 Отладка

### Backend
- Логи выводятся в консоль
- API доступен на `http://localhost:8080`
- Health check: `http://localhost:8080/health`

### Mobile
- Expo DevTools: `http://localhost:8081`
- React Native Debugger (опционально)
- Flipper (опционально)

## 🐛 Известные проблемы и решения

### Проблема: Mobile не может подключиться к backend
**Решение**: 
- Убедитесь, что backend запущен на порту 8080
- Для физических устройств измените `EXPO_PUBLIC_API_BASE` на IP адрес компьютера
- Проверьте настройки CORS в backend

### Проблема: TypeScript ошибки
**Решение**:
```bash
cd mobile
npx tsc --noEmit
```

### Проблема: Go модули не загружаются
**Решение**:
```bash
cd backend
go mod tidy
go mod download
```

## 📚 Документация

- [Техническое задание](spec.md) - Подробное описание требований
- [React Navigation](https://reactnavigation.org/) - Навигация в React Native
- [Expo](https://docs.expo.dev/) - Документация Expo
- [Gin](https://gin-gonic.com/) - Документация Gin framework

## 🤝 Вклад в проект

1. Fork репозитория
2. Создайте feature branch (`git checkout -b feature/amazing-feature`)
3. Commit изменения (`git commit -m 'Add amazing feature'`)
4. Push в branch (`git push origin feature/amazing-feature`)
5. Откройте Pull Request

## 📄 Лицензия

MIT License - см. файл [LICENSE](LICENSE) для деталей.

## 📞 Контакты

Для вопросов по разработке обращайтесь к команде разработки.

---

**Примечание**: Это MVP версия приложения. Для продакшена требуется дополнительная настройка безопасности, базы данных и интеграций.
