# Лабораторная работа №1

### 1.	Цель работы.

Получить опыт в разработке многопоточного клиент-серверного программного комплекса с использованием технологии TCP.

### 2.	Теоретическая часть.

Клиент (слой клиента) — это интерфейсный (обычно графический) компонент комплекса, предоставляемый конечному пользователю. Этот уровень не должен иметь прямых связей с базой данных (по требованиям безопасности и масштабируемости), быть нагруженным основной бизнес-логикой (по требованиям масштабируемости) и хранить состояние приложения (по требованиям надёжности). На этот уровень обычно выносится только простейшая бизнес-логика: интерфейс авторизации, алгоритмы шифрования, проверка вводимых значений на допустимость и соответствие формату, несложные операции с данными (сортировка, группировка, подсчёт значений), уже загруженными на терминал.

Сервер приложений (средний слой, связующий слой) располагается на втором уровне, на нём сосредоточена большая часть бизнес-логики. Вне его остаются только фрагменты, экспортируемые на клиента (терминалы), а также элементы логики, погруженные в базу данных (хранимые процедуры и триггеры). Реализация данного компонента обеспечивается связующим программным обеспечением. Серверы приложений проектируются таким образом, чтобы добавление к ним дополнительных экземпляров обеспечивало горизонтальное масштабирование производительности программного комплекса и не требовало внесения изменений в программный код приложения.

Сервер баз данных (слой данных) обеспечивает хранение данных и выносится на отдельный уровень, реализуется, как правило, средствами систем управления базами данных, подключение к этому компоненту обеспечивается только с уровня сервера приложений.

В простейших конфигурациях все компоненты или часть из них могут быть совмещены на одном вычислительном узле. В продуктивных конфигурациях как правило используется выделенный вычислительный узел для сервера баз данных или кластер серверов баз данных, для серверов приложений — выделенная группа вычислительных узлов, к которым непосредственно подключаются клиенты (терминалы).

[Трёхуровневая архитектура](https://ru.wikipedia.org/wiki/Трёхуровневая_архитектура)

### 3.	Ход выполнения работы.

Для выполнения работы понадобится два приложения: клиентская и серверная части. По условию варианта лабораторной работы, необходимо установить соединение клиента с сервером, передать строковое сообщение в формате “%n1%_%n2%_%n3%”, где %n% - любая строка без символа ‘_’, который является разделителем строк, поменять местами строки и вывести на стороне клиента.

Реализация [серверной части](https://github.com/Nis12/Lab1/blob/master/server.js) выполняется на языке JavaScript. Роль сервера будет играть Node.js – программная платформа, превращающая JavaScript из узкоспециализированного языка в язык общего назначения. Сервер будет принимать сообщение, обрабатывать его и отправлять результат клиенту.

Клиентом будет служить [приложение](https://github.com/Nis12/Lab1/blob/master/Client.cs), написанное на C#. Подключение осуществляется через Socket. Клиент отправляет сообщение и ждет результата его обработки от сервера.

### 4.	Вывод.

Входе проделанной работы было установлено TCP соединение через Socket. Реализация сервера позволила подключать и удерживать соединение с несколькими клиентами. Результат полученного сообщения от одного клиента отправляется всем подключенным клиентам.
