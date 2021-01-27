---
title: About fields
key: time-in-status
---

Все ниже представленные поля для расчёта времён позволяют
: делать расчеты используя рабочий календарь и временные зоны пользователей
Работать с данными в реальном времени - поиск, сортировка

с его помощью можно настроить мониторинг задач по времени в статусе, организовать очереди и рабочие столы, найти задачи требующие внимания.

Для всех полей можно составлять отчеты, собирать статистику, делать выгрузку и сравнивать их с контрольными величинами.

Для всех полей доступна настройка прав доступа и внешнего вида отображаемого значения.

Вы можете создавать неограниченное количество любых полей.

Общее описание полей
Time in status

считает время проведенное в указанном статусе или статусах.

- простая настройка

считает время для уже существующих задач и новых => Подходит для анализа старых задач.

- подходит для простых условий подсчета времени: только время проведённого в статусе или статусах.
- Не позволяет, считать останавливать или запускать отчёт времени по событиям( комментирование, указание значения в поле...). Только если задача будет менять статус при этих событиях. - в плагине нет встроенных инструментов для автоматизации.
-




Stopwatch
- Настройка сложнее, чем у time in status. Но нет ограничений замер времени только в статусе.
- Считает время между событиями(создание задачи, комментирование, установка значения в поля, переход в статус...)
  Например начать отчёт при создании задачи и остановить при создании комментария для автора или переходе в статус в работе.

-+ реагирует только на события которые произошли после настройки => не подходит для анализа старых задач
- Подходит для любых замеров времени. Большое количество готовых триггеров доступных в настройках. Возможность запускать и останавливать секундомеры вручную или через api.
- Позволяет запускать расчеты для задач удовлетворяющих условию - задается через jql.
- Может отправлять уведомления при смене состояния (при запуске,
  Остановке на паузу...)
- позволяет работать не только с отсчитанным временем но и со временем чародейном в состоянии паузы.

Timer
Реализован на базе секундомера и добавлено ограничение по времени. Ограничение например (4часа) устанавливается при запуске таймера(опционально может меняться при редактировании задачи)

Считает разницу(оставшееся время) между целевым временем(ограничением) и временем отсчитанным между событиями(как секундомер)

- Считает время между событиями и показывает сколько осталось от первоначального времени (Goal time - time between events)
  -+ реагирует только на события которые произошли после настройки => не подходит для анализа старых задач

Ограничения по времени(целевое время) настраиваются с помощью jql условий.
Например проект а и приоритет а ограничение 4часа
Проект а и приоритет б ограничение 8 часов

- позволяет работать не только с отсчитанным временем но и со временем чародейном в состоянии паузы, и оставшимся временем и временем потраченным сверх ограничений.



Так же для полей доступы дополнительные функции через вспомогательные поля и сравнение полей.

Если вам нужно рассчитать время между датами то обратите внимание на связку этого плагина и расчётные поля.  Поле позволяет расчитывать время между датами в том числе по рабочему календарю а так же позволяет создавать дополнительные расчётные поля по вашей формуле. 

