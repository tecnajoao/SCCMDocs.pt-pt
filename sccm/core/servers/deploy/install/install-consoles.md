---
title: "Установка консоли | Документы Майкрософт"
description: "Сведения об установке консоли Configuration Manager для подключения к сайту центра администрирования или первичному сайту."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 88ecbc48fd03ce988f04408d0378844cbed1de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>Установка консоли System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Администраторы используют консоль System Center Configuration Manager для управления средой Configuration Manager. Каждая консоль Configuration Manager может подключаться к сайту центра администрирования или первичному сайту. Консоль Configuration Manager нельзя подключить к вторичному сайту.

> [!NOTE]  
>  Объекты, отображаемые для администратора, который запускает консоль, зависят от разрешений, назначенных его учетной записи пользователя. Дополнительные сведения о ролевом администрировании см. в разделе [Основы ролевого администрирования для System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Вы можете установить консоль Configuration Manager во время установки сервера сайта в мастере установки или запустить автономное приложение установки, использующее мастер установки.  

 Приведенная ниже процедура используется для установки консоли Configuration Manager с помощью автономного приложения.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Установка консоли Configuration Manager с помощью мастера установки  

1.  Убедитесь в том, что выполняются перечисленные ниже требования.  

    -  У вас есть права **локального администратора** на компьютере, на котором будет запущена консоль.  

    -   У вас есть разрешения на **чтение** из расположения файлов установки консоли Configuration Manager.  

2.  Перейдите в одно из указанных ниже расположений.  

    -   На сервере сайта перейдите в папку **<*путь_установки_сервера_сайта_Configuration_Manager*>\Tools\ConsoleSetup**.  

    -   С исходного носителя Configuration Manager перейдите в папку **<*исходные_файлы_Configuration_Manager*>\Smssetup\Bin\I386**.  

    > [!TIP]  
    >  Рекомендуется запускать установку консоли Configuration Manager с сервера сайта, а не с установочного носителя System Center Configuration Manager. Процесс установки сервера сайта копирует установочные файлы консоли Configuration Manager и поддерживаемые языковые пакеты для сайта во вложенную папку **Tools\ConsoleSetup**. При установке консоли Configuration Manager с установочного носителя всегда устанавливается англоязычная версия, независимо от поддерживаемых языков на сервере сайта или языковых параметров операционной системы компьютера. Вы можете скопировать папку **ConsoleSetup** в другое расположение для запуска.

3.  Чтобы открыть мастер установки консоли Configuration Manager, дважды щелкните файл **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Всегда устанавливайте консоль Configuration Manager с помощью consolesetup.exe. Хотя для установки консоли Configuration Manager можно запустить файл adminconsole.msi, в этом случае проверка готовности и зависимостей не выполняется, поэтому существует вероятность некорректной установки.  

4.  В мастере нажмите кнопку **Далее**.  

5.  На странице **Сервер сайта** укажите полное доменное имя сервера сайта для подключения консоли Configuration Manager.  

6.  На странице **Папка установки** укажите папку установки для консоли Configuration Manager. Путь к папке не должен содержать конечные пробелы и символы Юникода.  

7.  На странице **Программа улучшения качества программного обеспечения** укажите, хотите ли вы принимать участие в программе улучшения качества программного обеспечения (CEIP).  

8.  На странице **Все готово для установки** нажмите кнопку **Установить**, чтобы установить консоль Configuration Manager.  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Установка консоли Configuration Manager из командной строки  

1.  На сервере, с которого будет установлена консоль Configuration Manager, откройте командную строку и перейдите в одно из следующих расположений:  

    -   **<*путь_установки_сервера_сайта_Configuration_Manager*>\Tools\ConsoleSetup**  

    -   **<*установочный_носитель_Configuration_Manager*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  При установке консоли Configuration Manager из командной строки всегда устанавливается англоязычная версия, независимо от языковых параметров операционной системы компьютера. Чтобы установить консоль Configuration Manager на другом языке, необходимо [использовать мастер установки](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  В командной строке введите **consolesetup.exe**. Выберите нужные параметры командной строки.  

|  .     | Описание     |
  | :------------- | :------------- |
  |/q|Автоматически устанавливает консоль Configuration Manager. Параметры **EnableSQM**, **TargetDir**и **DefaultSiteServerName** при использовании этого параметра являются обязательными.|  
  |/uninstall|Удаляет консоль Configuration Manager. При использовании совместно с параметром **/q** этот параметр следует указать первым.|  
  |LangPackDir|Указывает путь к папке, содержащей языковые файлы. Для скачивания языковых файлов вы можете использовать **загрузчик программы установки** . Если этот параметр не используется, программа установки выполнит поиск языковой папки в текущей папке. Если языковая папка найдена не будет, программа установки продолжит установку только для английского языка. Дополнительные сведения см. в разделе [Загрузчик программы установки](setup-downloader.md).|  
  |TargetDir|Указывает папку для установки консоли Configuration Manager. Этот параметр является обязательным при использовании параметра **/q** .|  
  |EnableSQM|Указывает, следует ли принимать участие в программе улучшения качества программного обеспечения. Чтобы присоединиться к программе, используйте значение **1**, а чтобы отказаться от участия — значение **0**. Этот параметр является обязательным при использовании параметра **/q** .|  
  |DefaultSiteServerName|Определяет полное доменное имя сервера сайта, к которому консоль подключается при открытии. Этот параметр является обязательным при использовании параметра **/q** .|  


  **Примеры:**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
