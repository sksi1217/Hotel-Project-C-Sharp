# Hotel-Project-C-Sharp

## 1. Структура проекта на C# WPF
### Основные модули:
1. Аутентификация и авторизация
   - Регистрация новых пользователей (администраторы, руководители).
   - Вход в систему с проверкой ролей.
   - Управление правами доступа.
2. Управление номерным фондом
   - Создание, редактирование и удаление информации о номерах.
   - Классификация номеров по типам (одноместный, двухместный, люкс и т.д.).
   - Отслеживание статусов номеров (свободен, занят, грязный, чистый).
3. Бронирование номеров
   - Поиск свободных номеров по датам.
   - Создание, редактирование и отмена бронирований.
   - Назначение номеров гостям.
4. Финансовые операции
   - Прием оплаты за проживание и дополнительные услуги.
   - Выставление счетов.
   - Формирование финансовых отчетов.
5. Управление персоналом
   - Создание графиков работы для уборочного персонала.
   - Распределение задач на уборку номеров.
   - Отслеживание выполнения задач.
6. Статистика и аналитика
   - Расчет показателей:
     - Процент загрузки номерного фонда.
     - ADR (Average Daily Rate).
     - RevPAR (Revenue Per Available Room).
     - Визуализация данных через графики и диаграммы.
7. Управление клиентами
   - Создание профилей клиентов.
   - Хранение истории бронирований.
   - Учет пожеланий и предпочтений.
8. Интеграция с PMS
   - Интеграция с системой управления бронированиями для автоматизации процессов.
9. Мобильное приложение для клиентов (необязательно)
   - Если требуется, можно создать мобильную версию на основе WPF или использовать Xamarin/MAUI для кроссплатформенной разработки.


## 2. Примерная архитектура проекта
### Проектная структура в Visual Studio:
```
/GuestHouseManagement
│
├── /GuestHouseManagement.App
│   ├── MainWindow.xaml         // Основное окно приложения
│   ├── LoginWindow.xaml        // Окно входа
│   ├── AdminDashboard.xaml     // Панель администратора
│   ├── ManagerDashboard.xaml   // Панель руководителя
│   └── ClientBooking.xaml      // Бронирование для клиентов
│
├── /GuestHouseManagement.Core
│   ├── Models                  // Модели данных (User, Room, Booking, etc.)
│   │   ├── User.cs
│   │   ├── Room.cs
│   │   └── Booking.cs
│   ├── Services                // Сервисы для бизнес-логики
│   │   ├── AuthService.cs
│   │   ├── RoomService.cs
│   │   └── BookingService.cs
│   └── Helpers                 // Вспомогательные классы (Encryption, Logging)
│
├── /GuestHouseManagement.Data
│   ├── DbContext.cs            // Контекст базы данных
│   ├── Repositories            // Репозитории для работы с данными
│   │   ├── UserRepository.cs
│   │   ├── RoomRepository.cs
│   │   └── BookingRepository.cs
│
└── /GuestHouseManagement.API   // API для интеграции с PMS
    ├── Controllers             // Контроллеры API
    │   ├── BookingController.cs
    │   └── RoomController.cs
    └── Startup.cs              // Настройка API
```


Вот описание того, что делает каждый класс и компонент в структуре проекта:

---

App : Отвечает за пользовательский интерфейс.
Core : Реализует бизнес-логику и управляет моделями данных.
Data : Обеспечивает работу с базой данных.
API : Предоставляет интерфейс для интеграции с внешними системами.

---

### **1. GuestHouseManagement.App**

#### **MainWindow.xaml**
- **Описание:** Основное окно приложения.
- **Функционал:**
  - Представляет главный интерфейс программы.
  - Содержит меню для перехода к различным разделам (например, панель администратора, панель руководителя, бронирование клиентов).

#### **LoginWindow.xaml**
- **Описание:** Форма входа в систему.
- **Функционал:**
  - Позволяет пользователям авторизоваться с использованием логина и пароля.
  - Проверяет роль пользователя (администратор, руководитель или клиент) и предоставляет доступ к соответствующим функциям.

#### **AdminDashboard.xaml**
- **Описание:** Панель управления для администратора гостиницы.
- **Функционал:**
  - Отображает информацию о бронированиях, номерах и клиентах.
  - Позволяет назначать номера, регистрировать оплату, создавать графики уборки и отслеживать статусы номеров.

#### **ManagerDashboard.xaml**
- **Описание:** Панель управления для руководителя гостиницы.
- **Функционал:**
  - Предоставляет доступ к статистике (процент загрузки, ADR, RevPAR).
  - Позволяет управлять персоналом и расписанием работ.
  - Отображает финансовые показатели и отчеты.

#### **ClientBooking.xaml**
- **Описание:** Интерфейс для бронирования номеров клиентами.
- **Функционал:**
  - Позволяет клиентам искать свободные номера по датам.
  - Создавать новые бронирования.
  - Оплачивать услуги через интегрированные платежные системы.

---

### **2. GuestHouseManagement.Core**

#### **Models**
- **User.cs**
  - **Описание:** Модель данных для пользователей.
  - **Функционал:**
    - Хранит информацию о пользователях (логин, пароль, роль, права доступа).
    - Поддерживает методы для работы с учетными записями.

- **Room.cs**
  - **Описание:** Модель данных для номеров гостиницы.
  - **Функционал:**
    - Хранит информацию о номерах (номер, тип, цена, статус).
    - Поддерживает методы для изменения статуса номера (свободен, занят, грязный, чистый).

- **Booking.cs**
  - **Описание:** Модель данных для бронирований.
  - **Функционал:**
    - Хранит информацию о бронировании (дата заезда/выезда, гость, номер, статус).
    - Поддерживает методы для создания, редактирования и отмены бронирований.

#### **Services**
- **AuthService.cs**
  - **Описание:** Сервис аутентификации и авторизации.
  - **Функционал:**
    - Проверяет логины и пароли пользователей.
    - Определяет роли пользователей (администратор, руководитель, клиент).
    - Обеспечивает безопасность входа в систему.

- **RoomService.cs**
  - **Описание:** Сервис управления номерами.
  - **Функционал:**
    - Ищет свободные номера по датам.
    - Изменяет статус номеров (свободен → занят → грязный → чистый).
    - Создает графики уборки и распределяет задачи между персоналом.

- **BookingService.cs**
  - **Описание:** Сервис управления бронированиями.
  - **Функционал:**
    - Создает новые бронирования.
    - Редактирует существующие бронирования.
    - Отменяет бронирования.
    - Выполняет проверку на наличие свободных номеров.

#### **Helpers**
- **Encryption.cs**
  - **Описание:** Класс для шифрования данных.
  - **Функционал:**
    - Шифрует пароли пользователей перед сохранением в базу данных.
    - Расшифровывает данные при необходимости.

- **Logging.cs**
  - **Описание:** Класс для ведения журнала событий.
  - **Функционал:**
    - Записывает действия пользователей (например, вход, изменение данных).
    - Сохраняет ошибки и исключения для последующего анализа.

---

### **3. GuestHouseManagement.Data**

#### **DbContext.cs**
- **Описание:** Контекст базы данных.
- **Функционал:**
  - Управляет соединением с базой данных.
  - Определяет модели (`User`, `Room`, `Booking`) как таблицы в базе данных.
  - Поддерживает CRUD операции (Create, Read, Update, Delete).

#### **Repositories**
- **UserRepository.cs**
  - **Описание:** Репозиторий для работы с пользователями.
  - **Функционал:**
    - Создает новых пользователей.
    - Проверяет существование пользователя по логину.
    - Обновляет данные пользователей.

- **RoomRepository.cs**
  - **Описание:** Репозиторий для работы с номерами.
  - **Функционал:**
    - Создает новые номера.
    - Получает список всех номеров.
    - Изменяет статус номера.

- **BookingRepository.cs**
  - **Описание:** Репозиторий для работы с бронированиями.
  - **Функционал:**
    - Создает новые бронирования.
    - Получает список бронирований по датам.
    - Отменяет бронирования.

---

### **4. GuestHouseManagement.API**

#### **Controllers**
- **BookingController.cs**
  - **Описание:** Контроллер для управления бронированиями через API.
  - **Функционал:**
    - Обрабатывает запросы на создание, обновление и удаление бронирований.
    - Возвращает список бронирований для внешних систем (например, PMS).

- **RoomController.cs**
  - **Описание:** Контроллер для управления номерами через API.
  - **Функционал:**
    - Обрабатывает запросы на получение информации о номерах.
    - Возвращает список свободных номеров по датам.

#### **Startup.cs**
- **Описание:** Конфигурация API.
- **Функционал:**
  - Настройка маршрутов для контроллеров.
  - Подключение middleware для безопасности (например, CORS, HTTPS).
  - Инициализация контекста базы данных.

---

### **Общий вывод**

Каждый класс и компонент в структуре проекта имеет четко определенную роль:
- **App**: Отвечает за пользовательский интерфейс.
- **Core**: Реализует бизнес-логику и управляет моделями данных.
- **Data**: Обеспечивает работу с базой данных.
- **API**: Предоставляет интерфейс для интеграции с внешними системами.

Эта структура обеспечивает модульность, масштабируемость и удобство поддержки проекта.
