---
page_type: sample
products:
- office-outlook
- office-365
languages:
- javascript
extensions:
  contentType: samples
  technologies:
  - Add-ins
  createdDate: 8/19/2015 11:13:31 AM
---
# Outlook-Add-in-Store-Custom-Properties-On-Exchange-Server
Это приложение задает свойство для электронного сообщения, а затем сохраняет его на сервере Exchange Server, чтобы вы могли получить его при следующем возврате элемента. Например, если ваша почтовая надстройка для Outlook добавляет контакты в базу данных внешних контактов, вы можете задать свойство элемента, чтобы показать, что контакт был добавлен так, чтобы вы не выводили запрос на добавление одного и того же контакта еще раз.

Метод [loadCustomPropertiesAsync](http://msdn.microsoft.com/library/dfbec151-8ea7-4915-b723-09ea1396a261) элемента "элемент" возвращает объект [CustomProperties](http://msdn.microsoft.com/library/%2095a69bd6-c4dc-429a-8b27-e2b68f74f3e3), который содержит и управляет настраиваемыми свойствами, хранящимися для элемента. После загрузки пользовательских свойств вы можете сделать следующее:

* Для чтения и создания настраиваемых свойств используйте метод [получить](http://msdn.microsoft.com/library/3ab90551-138a-482d-9d93-4cdb20db193b) и [установить](http://msdn.microsoft.com/library/03a8b253-b681-4a09-b828-80d9cf46ca9d). 
* Используйте метод [убрать](http://msdn.microsoft.com/library/01983beb-766f-4308-9e23-e840e950f7e3), чтобы удалить созданные вами пользовательские свойства. 
* Используйте метод [saveAsync](http://msdn.microsoft.com/library/690d5aa9-62b5-4e5c-9548-62dfdbb5fa56) для сохранения любых изменений, которые вы внесли обратно на сервер Exchange. 

Вы должны вызвать метод [saveAsync](http://msdn.microsoft.com/library/690d5aa9-62b5-4e5c-9548-62dfdbb5fa56), чтобы сохранить свойства на сервере Exchange; в противном случае все внесенные вами изменения отменяются при изменении текущего элемента.

Пример пользовательского интерфейса имеет три страницы: одну для установки ключа и значения настраиваемого свойства, одну для получения значения настраиваемого свойства и одну для удаления настраиваемых свойств или сохранения изменений, которые вы вносите в сервер Exchange.

Файл JavaScript содержит обработчики нажатий для кнопок в пользовательском интерфейсе для получения, установки, удаления и сохранения пользовательских свойств с помощью соответствующих методов объекта [CustomProperties](http://msdn.microsoft.com/library/%2095a69bd6-c4dc-429a-8b27-e2b68f74f3e3). Локальная логическая переменная customPropertiesAreLoaded задается в функции ответного вызова метода loadCustomPropertiesAsync, чтобы показать, что объект настраиваемых свойств загружен. Обработчики проверяют это значение, чтобы убедиться в том, что объект [CustomProperties](http://msdn.microsoft.com/library/%2095a69bd6-c4dc-429a-8b27-e2b68f74f3e3) доступен перед вызовом функций объекта. 

*Предварительные требования*

Этот образец требует, чтобы у вас было следующее:

* Visual Studio 2012 с приложениями для шаблонов проектов Office. 
* Компьютер под управлением Exchange 2013 с хотя бы одной учетной записью электронной почты или учетной записью разработчика Office 365. Вы можете [присоединиться к Программе разработчика Office 365 и получить бесплатную годовую подписку на Office 365](https://aka.ms/devprogramsignup).
* Опыт программирования на JavaScript и работы с веб-службами. 
* Internet Explorer 9 или Internet Explorer 10 Preview. 

*Ключевые компоненты примера*

Пример решения содержит следующие файлы:

* Проект CustomProperties 
  * CustomProperties.xml - файл манифеста для почтовой надстройки для Outlook. 
* CustomPropertiesWeb проект
  * Home.html - пользовательский интерфейс HTML для почтовой надстройки для Outlook. 
  * Home.js - файл JavaScript, который обрабатывает запрос и использование запроса веб-служб Exchange (EWS). 
  * Скрипты \ Lib - почтовый модуль для Outlook и API Outlook Web App. 


*Настройка примера*

Почтовая надстройка будет активирована для любого сообщения электронной почты в папке «Входящие» пользователя. Вы можете упростить тестирование надстройки, отправив одно или несколько сообщений электронной почты в свою тестовую учетную запись перед запуском образца.

*выполнить сборку кода из примера;*

Нажмите F5, чтобы создать и развернуть пример приложения. Для развертывания приложения выполните следующие задачи:

1. Подключитесь к учетной записи Exchange, указав адрес электронной почты и пароль для сервера Exchange 2013. 
2. Разрешить серверу настроить учетную запись электронной почты. 

*Запуск и проверка примера*

Вы запускаете и тестируете образец в веб-браузере, который запускается Visual Studio при создании и развертывании образца.

Если вы запускаете образец на сервере Exchange, который использует самозаверяющий сертификат по умолчанию, вы получите ошибку сертификата при запуске веб-браузера. Убедившись, что веб-браузер открывает правильный URL-адрес, просмотрев веб-адрес, вы можете нажать Продолжить на этом веб-сайте, чтобы запустить Outlook Web App.

Выполните следующие шаги для запуска образца:

1. Войдите в учетную запись электронной почты, введя имя учетной записи и пароль. 
2. Выберите сообщение в папке «Входящие». 
3. Подождите, пока панель приложения появится над сообщением. 
4. На панели приложений нажмите Пользовательские свойства. 
5. Когда появится надстройка электронной почты с настраиваемыми свойствами, введите имя и значение свойства в текстовые поля, а затем нажмите кнопку «Сохранить», чтобы сохранить значение свойства. 
6. Нажмите кнопку «Получить», введите имя свойства и нажмите кнопку «Получить», чтобы получить свойство. 
7. Нажмите «Управление» и либо «Сохранить», чтобы сохранить сохраненные свойства на сервере Exchange, либо введите имя свойства и нажмите «Удалить», чтобы удалить свойство из хранилища. 

*Устранение неполадок*

Ниже перечислены распространенные ошибки, которые могут возникнуть при использовании Outlook Web App для проверки почтовой надстройки для Outlook:

* Панель приложения не отображается при выборе сообщения. В этом случае перезапустите приложение, выбрав «Отладка - Остановить отладку» в окне Visual Studio, затем нажмите клавишу F5, чтобы перестроить и развернуть приложение. 
* Изменения в коде JavaScript могут не учитываться при развертывании и запуске приложения. Если изменения не получены, очистите кэш в веб-браузере, выбрав «Сервис» - «Свойства обозревателя» и нажав кнопку «Удалить…». Удалите временные файлы Интернета, а затем перезапустите приложение. 

*Дополнительные ресурсы*

* [Дополнительные примеры надстроек](https://github.com/OfficeDev?utf8=%E2%9C%93&query=-Add-in)
* [Объект CustomProperties](http://msdn.microsoft.com/library/%2095a69bd6-c4dc-429a-8b27-e2b68f74f3e3)
* [loadCustomPropertiesAsync method](http://msdn.microsoft.com/library/dfbec151-8ea7-4915-b723-09ea1396a261)
* [метод Получить](http://msdn.microsoft.com/library/3ab90551-138a-482d-9d93-4cdb20db193b)
* [метод Установить](http://msdn.microsoft.com/library/03a8b253-b681-4a09-b828-80d9cf46ca9d)
* [метод Удалить](http://msdn.microsoft.com/library/01983beb-766f-4308-9e23-e840e950f7e3)
* [метод saveAsync](http://msdn.microsoft.com/library/690d5aa9-62b5-4e5c-9548-62dfdbb5fa56)



Этот проект соответствует [Правилам поведения разработчиков открытого кода Майкрософт](https://opensource.microsoft.com/codeofconduct/). Дополнительные сведения см. в разделе [часто задаваемых вопросов о правилах поведения](https://opensource.microsoft.com/codeofconduct/faq/). Если у вас возникли вопросы или замечания, напишите нам по адресу [opencode@microsoft.com](mailto:opencode@microsoft.com).