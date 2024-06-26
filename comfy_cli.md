# Установка интерфейса командной строки "Comfy" 
Существует кросс-платформенный интерфейс управления ComfyUI в режиме "командной строки Comfy", с которым мы сейчас м познакомимся.

Все примеру тут приведены исходя из того, что питон у нас находится по пути **"c:\p311"** (версия 3.11), а устанавливать **Comfy** мы будем в папку **"d:\3"**.

Для начала создадим "виртуальное окружение" питона "venv" *(но можно и просто в любого питона, это не принципиально, т.к. все команды я буду давать в универсальной нотации, и они подойдут как для системного, так и для venv и портабельного питона)*:

    c:\p311\python -m venv d:\3\venv
	
<p align="center">Если мы все правильно сделали, то у нас по адресу "d:\3"появится папка "venv" со следующим содержимым:</p>

<p align="center">
  <img src="img_cli/000.jpg">
</p>

Запомним, что вызывать питона из этой установки нам надо командой:

    d:\3\venv\Scripts\python

... и все обращения к питону мы будем производить именно этой командой, с указанием полного пути к нему.

>Примечание:
>Если у вас питон стоит по другому адресу, то замените просто путь "d:\3\venv\Scripts\" на свой.
>Я пишу тут полные пути для того, чтобы можно было повторить эти команды, просто копируя их из со страницы.

<p align="center">
  <img src="img_cli/001.jpg">
</p>

Итак, у нас установлен "чистый" питон, без всяких пакетов. Новая идеология установки Comfy заключается в следующем:

<p align="center"><b>Устанавливаем "Comfy-Cli" - инструмент командной строки для ComfyUI</b></p>

    d:\3\venv\Scripts\python -m pip install comfy-cli
	
Питон немного повозится, и установит нужные пакеты питона и новые компоненты.

<p align="center">
  <img src="img_cli/002.jpg">
</p>

В лучших традициях "а вдруг кто не помнит" файлы продублированы с разными именами. Если у вас память хорошая, можете оставить только тот, чье название точно помините.

Пошаманим немного, и выполним такую команду:

    d:\3\venv\Scripts\Comfy

... и получим справку по управлению Comfy из режима командной строки. Запросим номер версии (см.фото)

<p align="center">
  <img src="img_cli/003.jpg">
</p>

Теперь управление Comfy можно производить отсюда.

Выполняем команды:

    d:\3\venv\Scripts\comfy install
	
... и начнется установка ComfyUI в папку "Документы\comfy\ComfyUI" (%DocumentsFolder%\comfy\ComfyUI) текущего пользователя.
	
Меня это не совсем устраивает, мне не нравится место, куда он мне "задвинул" комфи, поэтому я делаю так:

    xcopy /V /D /S /E /H c:\Users\ИМЯ_АККАУНТА\Documents\comfy\ComfyUI d:\3\ComfyUI\
	rd /s /q  c:\Users\ИМЯ_АККАУНТА\Documents\comfy\ComfyUI
	
Это переместит все, что установилось в папку "d:\3" где у нас уже находится папка "venv".

>Примечание:
>Перемещение не обязательно, если вы хотите, то можете продолжать работать и так, это я делаю для того, чтобы было понятно, как можно изменить место расположения комфи.

После того, как мы переместили комфи, дадим следующую команду:

    d:\3\venv\Scripts\comfy set-default d:\3\ComfyUI

<p align="center">
  <img src="img_cli/004.jpg">
</p>

Эта команда установит указанную нами папку с комфи на "папка по умолчанию".

>Примечание:
>В качестве "Default ComfyUI workspace" выбирать уже существующую на диске ComfyUI, если она скачана с git...
>Надо установить "pip install comfy_cli" в питона уже существующей ComfyUI, потом командой "comfy set-default path" где path - путь к существующему ComfyUI, то получим интерфейс командой строки для управления, запуска, обновления, установки пакетов, нод, модулей и т.п. через интерфейс командной строки.

Выполним команду:

    d:\3\venv\Scripts\comfy env

... и получим окно с текущими настройками Comfy.

<p align="center">
  <img src="img_cli/005.jpg">
</p>

Следующая команда запускает ComfyUI:

    d:\3\venv\Scripts\comfy launch
	
<p align="center">
  <img src="img_cli/006.jpg">
</p>
	
Запускаем браузер:

    http://127.0.0.1:8188
	
... и видим знакомый интерфейс:

<p align="center">
  <img src="img_cli/007.jpg">
</p>

Понятно, что "первый блин комом", это мой первый запуск системы таким образом... много непоняток.

И все же она словила "птичку Обломинго" не сумев САМА на чистом питоне (!) нормально поставить все пакеты питона (((

<p align="center">
  <img src="img_cli/008.jpg">
</p>


# Установка comfy_cli "на дурачка"

Собственно говоря, весь "путь" от установки самого "comfy_cli" и до запуска ComfyUI можно пройти следующими командами, только первая из которых "в питоне" и устанавливает в питона сам пакет "comfy_cli":

    \venv\Scripts\python -m pip install comfy_cli

Дальше мы уже не имеем дело с самим питоном, а все управление Comfy производится EXE-шником с именем "comfy.exe", который инсталлируется в папку скриптов (если это venv), вызывается оттуда и ему
 в качестве аргументов дается указание что именно сделать *(в примере ниже "Установить ComfyUI по умолчанию")*:

    \venv\Scripts\comfy install

И дальше уже можно запустить только что установленный ComfyUI *(в примере с аргументом автозапуска браузера)*:

    \venv\Scripts\comfy launch -- --auto-launch
	
Собственно и все, что нужно для установки и запуска ComfyUI )))	

Дальше можно пользоваться всем спектром команд пакета comfy_cli:

    \venv\Scripts\comfy update comfy
    \venv\Scripts\comfy update all
	\venv\Scripts\comfy node show installed
	\venv\Scripts\comfy node show all
	
... и т.п., смотрите документацию на https://github.com/Comfy-Org/comfy-cli

# Установка comfy_cli на рабочую версию ComfyUI

Множественные эксперименты с инсталляцией/деинсталляцией comfy_cli могут привести к непоняткам, т.к. файл параметров comfy_cli остается "вне поля зрения", имеется в единственном экземпляре, и расположен по пути:

    \Users\USER_NAME\AppData\Local\comfy-cli\config.ini
	
Соответственно, если у вас несколько копий питона, и в каждый вы установили по экземпляру comfy_cli, все они будут брать информацию о настройках из одного файла. что может привести к непониманию "Я же удалил! Откуда он все это берет?!".

Поэтому помните, что "для сброса" всех параметров вам надо удалить еще и папку с этим файлом!

Заодно проверьте папку "Domcuments\comfy", куда он "по умолчанию" ставит ComfyUI после установки.

Итак, идем в виртуальное окружение "venv", папка "Scripts", и первым делом установим comfy_cli:

    venv\Srcipts\pyhton -m pip install comfy_cli
	
Потом мы уже просто вызываем по полному пути файл "comfy.exe" и в качестве аргументов командной строки передаем ему параметры и команды:

    venv\Scripts\comfy launch -- --auto-launch
	
Если до установки comfy_cli в питоне вы удалили файл конфигурации "\Users\USER_NAME\AppData\Local\comfy-cli\config.ini", то comfy_cli настроится автоматически на тот экземпляр ComfyUI, который работает на этом venv, и все команды управления comfy будут направлены именно этому экземпляру ComfyUI.

Таким образом мы получаем "интерфейс командной строки для управления ComfyUI" без вмешательства в код и работу самого ComfyUI.

Собственно и все.

Ставьте, учите команды терминала Comfy. Если раньше все можно было руководить ComfyUI командами питона, то теперь появился "менеджер командной строки Comfy".

Как файл "command.com" является "интерпретатором командной строки DOS", там теперь файл "comfy.exe" является "интерпретатором командной строки Comfy".

Не забывайте посматривать на текущие параметры настройки "comfy.exe":

    \venv\Scripts\comfy env
	
<p align="center">
  <img src="img_cli/009.jpg">
</p>
	
Да, еще: при первом запуске (перед созданием файла конфигурации он спросит:

    Do you agree to enable tracking to improve the application? [y/N]: y
	
Ответьте "Y".

Это всего лишь параметр, позволяющий разработчикам вести статистику количества установок Comfy.	

<p align="center">
  <img src="img_cli/010.jpg">
</p>

Удачи! )))

Оригинал документации: https://github.com/Comfy-Org/comfy-cli
