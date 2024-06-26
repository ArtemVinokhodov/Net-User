
Netty — асинхронный фреймворк сетевых приложений,
управляемых событиями.

Netty — это NIO клиент-серверный фреймворк, который позволяет
быстро и легко разрабатывать сетевые приложения, такие как
протокольные серверы и клиенты.
Это значительно упрощает и оптимизирует сетевое программирование,
такое как сервер сокетов TCP и UDP.

https://netty.io/

Основная цель Netty — построение высокопроизводительных
протокольных серверов на основе NIO с разделением и слабой
связью компонентов сети и бизнес-логики.

Channel — основа Java NIO. Представляет собой открытое соединение,
способное выполнять операции ввода-вывода, такие, как чтение и запись.

Каждая операция ввода-вывода на канале в Netty является неблокирующей.

Это означает, что каждая операция возвращается сразу после вызова.
В стандартной библиотеке Java есть интерфейс Future, но он не удобен
для целей Netty — мы можем только спросить Future о завершении операции
или заблокировать текущий поток до выполнения операции.

Вот почему у Netty есть собственный интерфейс ChannelFuture.
Можем передать обратный вызов ChannelFuture, который будет вызван
после завершения операции.

Netty использует парадигму приложений, управляемых событиями (Events),
поэтому конвейер обработки данных представляет собой цепочку событий,
проходящих через обработчики (Handlers). События и обработчики могут
быть связаны с входящим и исходящим потоком данных.

Входящие события могут быть следующими:
- Активация и деактивация канала
- Чтение событий операции
- Исключительные события
- Пользовательские события

Исходящие события проще и, как правило, связаны с открытием/закрытием
соединения и записью/удалением данных.

Приложения Netty состоят из нескольких сетевых событий и событий логики
приложений и их обработчиков. Базовыми интерфейсами для обработчиков
событий канала являются ChannelHandler и его преемники
ChannelOutboundHandler и ChannelInboundHandler.

Netty предоставляет огромную иерархию реализаций ChannelHandler.

Адаптеры являются пустыми реализациями, например,
ChannelInboundHandlerAdapter и ChannelOutboundHandlerAdapter.
Можем расширить эти адаптеры, когда нужно обработать некоторые события.


Кодеры (Encoders) и декодеры (Decoders). Поскольку работаем с сетевым
протоколом, необходимо выполнить сериализацию и десериализацию данных.
Для этой цели Netty вводит специальные расширения ChannelInboundHandler
для декодеров, способных декодировать входящие данные. Базовым классом
большинства декодеров является ByteToMessageDecoder.

Для кодирования исходящих данных у Netty есть расширения
ChannelOutboundHandler, называемые кодировщиками.
MessageToByteEncoder является основой для большинства реализаций
кодировщика. Можем преобразовать сообщение из последовательности
байтов в объект Java и наоборот, с помощью кодировщиков и декодеров.

---------------------------------------------------------------------

Тестируем приложение. Запускаем сперва сервер, потом клиент.
