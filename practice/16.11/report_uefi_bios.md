# Отчёт: 10 задач по BIOS/UEFI в Lenovo BIOS Simulator Center

Симулятор: https://download.lenovo.com/bsco/index.html

Устройство: ThinkPad T14s Gen 5, графический режим.

---

## Задача 1. Навигация по основным разделам

Открыл по очереди разделы Main, Config, Date/Time, Security, Startup, Restart.

В Main отображается:
- UEFI BIOS Version: N46ET09W
- UEFI BIOS Date: 2024-01-22
- Machine Type Model: 21LS
- System-unit serial number: PF12345
- System board serial number: L112345678
- CPU Type: Intel(R) Core(TM) CPU
- CPU Speed: 1.X00GHz
- Installed memory: 8192MB
- UEFI Secure Boot: On

![Main](screenshots/01_main.jpg)

Config: Network, USB, Keyboard/Mouse, Display, Power, Beep and Alarm, CPU, Thunderbolt 4, Intel AMT.

![Config](screenshots/01_config.jpg)

Date/Time: системные дата и время.

![Date/Time](screenshots/01_datetime.jpg)

Security: Password, Fingerprint, Security Chip, Virtualization, Secure Boot и другие.

![Security](screenshots/01_security.jpg)

Startup: Boot, Network Boot, Boot Mode, Option key Display, Boot device List F12 Option, Boot Order Lock.

![Startup](screenshots/01_startup.jpg)

Restart: Exit Saving Changes, Exit Discarding Changes, Load Factory Defaults и другие.

![Restart](screenshots/01_restart.jpg)

Где находятся настройки из задач 2–5:
- порядок загрузки: Startup
- Secure Boot: Security
- пароль супервизора: Security
- сброс настроек: Restart

---

## Задача 2. Смена порядка загрузки

Путь: Startup -> Boot

Исходный порядок:

![До](screenshots/02_boot_before.jpg)

Перетащил USB HDD на первое место, NVMe0 на второе:

![После](screenshots/02_boot_after.jpg)

Нажал F10 и подтвердил сохранение:

![F10](screenshots/02_save_confirm.jpg)

После повторного входа порядок сохранился:

![Повторный вход](screenshots/02_boot_reentry.jpg)

---

## Задача 3. Включение/выключение Secure Boot

Путь: Security -> Secure Boot -> Secure Boot

Исходный статус On:

![On](screenshots/03_secureboot_on.jpg)

Переключил в Off:

![Off](screenshots/03_secureboot_off.jpg)

Вернул в On:

![On снова](screenshots/03_secureboot_restored.jpg)

Перезагрузка сразу не требуется, изменение применяется после сохранения через F10.

Secure Boot проверяет цифровую подпись загрузчика ОС и не даёт запустить неподписанный или подменённый загрузчик. Это защита от буткитов и руткитов.

---

## Задача 4. Установка пароля супервизора

Путь: Security -> Password -> Supervisor Password

Исходно пароль не установлен:

![Пароли](screenshots/04_password_page.jpg)

Ввёл пароль Test1234 и подтверждение:

![Ввод](screenshots/04_password_enter.jpg)

Статус изменился на Enabled:

![Enabled](screenshots/04_password_enabled.jpg)

Изменил другую настройку. Запрос пароля в симуляторе не появился, симулятор это не эмулирует. На реальном ноутбуке пароль запрашивается при входе в BIOS.

![Изменение настройки](screenshots/04_change_setting.jpg)

Попытался снять пароль, оставив поля пустыми. Симулятор не принимает пустой пароль:

![Ошибка](screenshots/04_password_empty_error.jpg)

Пароль снят через Restart -> Load Factory Defaults, см. задачу 5.

---

## Задача 5. Сброс на заводские настройки

Путь: Restart -> Load Factory Defaults. Также есть клавиша F9.

![Подтверждение](screenshots/05_factory_confirm.jpg)

Порядок загрузки вернулся к исходному:

![Boot](screenshots/05_boot_reset.jpg)

Пароль супервизора снят, Secure Boot включён:

![Пароль](screenshots/05_password_reset.jpg)

---

## Задача 6. Управление встроенными устройствами

Путь: Config -> USB -> Always On USB

Пункта USB BIOS Support на этой модели нет, есть Always On USB.

Исходно On:

![On](screenshots/06_usb_on.jpg)

Отключил:

![Off](screenshots/06_usb_off.jpg)

Включил обратно:

![On снова](screenshots/06_usb_restored.jpg)

---

## Задача 7. Режим работы SATA/NVMe

Выполнить не получилось, поскольку в интерфейсе в разделе Config нет пункта Storage.

![Config](screenshots/01_config.jpg)

---

## Задача 8. Временное меню загрузки

Путь: Startup -> Boot Mode и Startup -> Boot device List F12 Option

![Startup](screenshots/08_startup_options.jpg)

Переключил Boot Mode в Diagnostics и отключил F12 Option:

![Изменено](screenshots/08_diagnostics_f12_off.jpg)

Вернул Quick и включил F12 Option:

![Возвращено](screenshots/08_restored.jpg)

Порядок в Startup -> Boot сохраняется и действует при каждой загрузке. Меню F12 позволяет выбрать устройство только для одной загрузки и сохранённые настройки не меняет.

---

## Задача 9. Просмотр системных логов

Путь: Main -> BIOS Event log

Раздела Config -> Diagnostics на этой модели нет. Журнал находится в Main, но симулятор его не поддерживает, пункта Clear Event Log тоже нет.

![Event log](screenshots/09_event_log.png)

---

## Задача 10. Подготовка к переустановке ОС

Шаг 1. Сброс через Restart -> Load Factory Defaults:

![Шаг 1](screenshots/10_1_factory.jpg)

Шаг 2. Secure Boot включён:

![Шаг 2](screenshots/10_2_secureboot.jpg)

Шаг 3. Установлен Supervisor Password:

![Шаг 3](screenshots/10_3_password.jpg)

Шаг 4. USB HDD поставлен первым:

![Шаг 4](screenshots/10_4_usb_first.jpg)

Шаг 5. Сохранение через F10:

![Шаг 5](screenshots/10_5_save.jpg)

Шаг 6. Повторный вход, настройки сохранились:

![Проверка порядка](screenshots/10_6a_check_boot.jpg)

![Проверка пароля](screenshots/10_6b_check_password.jpg)

Вернул исходный порядок загрузки:

![Порядок возвращён](screenshots/10_6c_boot_restored.jpg)

Клавиша F9 пароль не сняла:

![F9](screenshots/10_6d_f9_password_kept.jpg)

Пароль снят через Restart -> Load Factory Defaults:

![Пароль снят](screenshots/10_6e_password_removed.jpg)

---

## Пути к настройкам

- Startup -> Boot
- Security -> Secure Boot -> Secure Boot
- Security -> Password -> Supervisor Password
- Restart -> Load Factory Defaults
- Config -> USB -> Always On USB
- Startup -> Boot Mode
- Startup -> Boot device List F12 Option
- Main -> BIOS Event log
- F9 — сброс по умолчанию, F10 — сохранить и выйти
