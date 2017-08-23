---
title: "Настройка образов загрузки в Configuration Manager | Документы Майкрософт"
description: "Сведения о нескольких способах настройки образа загрузки с помощью Configuration Manager или средства командной строки DISM."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: ab2ecb64c9c80b4effed79ba08769c99473db0c4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="customize-boot-images-with-system-center-configuration-manager"></a>Настройка образов загрузки для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Каждая версия Configuration Manager поддерживает определенную версию комплекта средств для развертывания и оценки Windows (Windows ADK). Загрузочные образы можно обслуживать или настраивать в консоли Configuration Manager, если они были созданы на основе версии среды предустановки Windows из поддерживаемой версии Windows ADK. Для настройки остальных загрузочных образов необходимо использовать другой подход, например программу командной строки "Система обслуживания образов развертывания и управления ими (DISM)", которая входит в состав Windows AIK и Windows ADK.  

 Ниже приведены поддерживаемая версия Windows ADK, версия среды предустановки Windows, используемая как основа образа загрузки, который может быть настроен в консоли Configuration Manager, и версии среды предустановки Windows, используемые как основа образов загрузки, которые могут быть настроены с помощью DISM, а затем добавлены в Configuration Manager.  

-   **Версия Windows ADK**  

     Windows ADK для Windows 10  

-   **Версии среды предустановки Windows для загрузочных образов с возможностью настройки в консоли Configuration Manager**  

     Windows PE 10  

-   **Поддерживаемые версии среды предустановки Windows для загрузочных образов без возможности настройки в консоли Configuration Manager**  

     Среда предустановки Windows 3.1<sup>1</sup> и среда предустановки Windows 5  

     <sup>1</sup> Образ загрузки можно добавить в Configuration Manager, только если он был создан на основе среды предустановки Windows 3.1. Установите дополнительный компонент Windows AIK для Windows 7 с пакетом обновления 1 (SP1), чтобы обновить Windows AIK для Windows 7 (на основе среды предустановки Windows 3) с помощью дополнительного компонента Windows AIK для Windows 7 с пакетом обновления 1 (SP1) (на основе среды предустановки Windows 3.1). Дополнительный компонент Windows AIK для Windows 7 с пакетом обновления 1 (SP1) можно загрузить из [Центра загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=5188).  

     Например, если используется Configuration Manager, загрузочные образы из Windows ADK для Windows 10 (на основе среды предустановки Windows 10) можно настраивать в консоли Configuration Manager. Однако несмотря на то что загрузочные образы на основе Windows PE 5 поддерживаются, их необходимо настраивать с другого компьютера и использовать версию DISM, установленную вместе с Windows ADK для Windows 8. После этого загрузочный образ можно будет добавить в консоль Configuration Manager.  

 В этой статье описаны процедуры добавления дополнительных компонентов, необходимых для работы Configuration Manager, в загрузочный образ с помощью следующих пакетов среды предустановки Windows.  

-   **WinPE-WMI**. Добавляет поддержку инструментария управления Windows (WMI).  

-   **WinPE-Scripting**. Добавляет поддержку сервера сценариев Windows (WSH).  

-   **WinPE-WDS-Tools**. Устанавливает средства служб развертывания Windows.  

 Для добавления также доступны другие пакеты среды предустановки Windows. Дополнительные сведения о дополнительных компонентах, которые могут быть добавлены в загрузочный образ, см. на следующих ресурсах.  

-   Для среды Windows PE 5 см. раздел [WinPE: добавление пакетов (Справочник по дополнительным компонентам)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

-   Для среды предустановки Windows 3.1 см. статью [Добавление пакета в образ Windows PE](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) в библиотеке документации TechNet по Windows 7.  

> [!NOTE]
>При загрузке WinPE из настроенного образа загрузки, содержащего добавленные вами инструменты, можно открыть командную строку в WinPE и ввести имя файла инструмента, чтобы запустить его. Расположение этих инструментов автоматически добавляется в переменную path. Командную строку можно добавить, только если на вкладке **Настройка** свойств образа загрузки выбран параметр **Включить поддержку командной строки (только для проверки)**.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Настройка образа загрузки, использующего среду предустановки Windows 5  
 Чтобы настроить загрузочный образ, использующий Windows PE 5, необходимо установить Windows ADK и использовать программу командной строки DISM для подключения загрузочного образа, добавления дополнительных компонентов и драйверов и фиксации изменений в загрузочном образе. Ниже описана процедура настройки загрузочного образа.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Процедура настройки загрузочного образа, использующего среду предустановки Windows 5  

1.  Установите Windows ADK на компьютере, на котором не установлена другая версия Windows AIK или Windows ADK и отсутствуют какие-либо компоненты Configuration Manager.  

2.  Скачайте Windows ADK для Windows 8.1 из [Центра загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=39982).  

3.  Скопируйте образ загрузки (wimpe.wim) из папки установки WindowsADK (например, <*путь_установки*>\Windows Kits\\\<*версия*>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<*x86 или amd64*>\\<*язык*>) в конечную папку на компьютере, с которого будет выполняться настройка загрузочного образа. В этой процедуре в качестве имени конечной папки используется C:\WinPEWAIK.  

4.  Используйте DISM для подключения загрузочного образа к локальной папке среды предустановки Windows. Например, введите следующую команду:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     где C:\WinPEWAIK — папка, содержащая загрузочный образ, а C:\WinPEMount — папка подключения.  

    > [!NOTE]
    >  Дополнительные сведения о DISM см. в статье [Техническое руководство по системе обслуживания образов развертывания и управления ими (DISM)](http://technet.microsoft.com/library/hh824821.aspx) в библиотеке документации TechNet по Windows 8.1 и Windows 8.

5.  После подключения загрузочного образа используйте DISM для добавления в него дополнительных компонентов. В среде предустановки Windows 5 64-разрядные дополнительные компоненты находятся в папке <*путь_установки*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

    > [!NOTE]
    >  В этой процедуре используется следующее расположение дополнительных компонентов: C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. Используемый путь может отличаться в зависимости от версии и параметров установки Windows ADK.  

     Введите следующие команды для установки дополнительных компонентов:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<язык\>* **\WinPE-SecureStartup_** *<язык\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<язык\>* **\WinPE-WMI_** *<язык\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<язык\>* **\WinPE-Scripting** *<язык\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<язык\>* **\WinPE-WDS-Tools_** *<язык\>* **.cab"**  

     Где C:\WinPEMount — подключенная папка, а языковой стандарт — языковой стандарт для компонентов. Например, для языкового стандарта **en-us** следует ввести:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

    > [!TIP]
    >  Дополнительные сведения о дополнительных компонентах, которые могут быть добавлены в загрузочный образ, см. в статье [Справочник по дополнительным компонентам среды предустановки Windows](http://technet.microsoft.com/library/hh824926.aspx) в библиотеке документации TechNet по Windows 8.1 и Windows 8.  

6.  Используйте DISM для добавления в загрузочный образ специальных драйверов, если это необходимо. Введите следующую команду для добавления в загрузочный образ драйверов:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *путь_к_INF-файлу_драйвера* **>**  

     где C:\WinPEMount — папка подключения.  

7.  Введите следующую команду, чтобы отключить файл загрузочного образа и зафиксировать изменения:  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     где C:\WinPEMount — папка подключения.  

8.  Добавьте обновленный загрузочный образ в Configuration Manager, чтобы он стал доступным для использования в последовательностях задач. Чтобы импортировать обновленный загрузочный образ, выполните следующие действия.  

    1.  В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.  

    2.  В рабочей области **Библиотека программного обеспечения** разверните узел **Операционные системы**и выберите **Загрузочные образы**.  

    3.  На вкладке **Главная** в группе **Создать** щелкните элемент **Добавить загрузочный образ** , чтобы запустить мастер добавления загрузочного образа.  

    4.  На странице **Источник данных** настройте следующие параметры, затем нажмите кнопку **Далее**.  

        -   В поле **Путь** укажите путь к обновленному файлу загрузочного образа. Указанный путь должен быть допустимым сетевым путем в формате UNC. Например: **\\\\<***имя_сервера***>\\<***общая папка WinPEWAIK***>\winpe.wim**.  

        -   В раскрывающемся списке **Загрузочный образ** выберите загрузочный образ. Если в WIM-файле содержится несколько загрузочных образов, все они указываются в списке.  

    5.  На странице **Общие** укажите следующие параметры и нажмите кнопку **Далее**.  

        -   В поле **Имя** введите уникальное имя загрузочного образа.  

        -   В поле **Версия** введите номер версии загрузочного образа.  

        -   В поле **Комментарий** введите краткое описание порядка использования загрузочного образа.  

    6.  Завершите работу мастера.  

9. Можно включить в загрузочном образе командную оболочку для его отладки и устранения неполадок в среде предустановки Windows. Чтобы включить командную оболочку, выполните следующие действия.  

    1.  В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.  

    2.  В рабочей области **Библиотека программного обеспечения** разверните узел **Операционные системы**и выберите **Загрузочные образы**.  

    3.  Найдите в списке новый загрузочный образ и определите для него ИД пакета. ИД пакета можно найти в столбце **Идентификатор образа** напротив загрузочного образа.  

    4.  В командной строке введите команду **wbemtest** , чтобы открыть тестер инструментария управления Windows.  

    5.  Введите **\\\\<***компьютер_поставщика_SMS***>\root\sms\site_<***код_сайта***>** в поле **Пространство имен** и нажмите кнопку **Подключить**.  

    6.  Нажмите кнопку **Открыть экземпляр**, введите **sms_bootimagepackage.packageID="<ИД_пакета\>"** и нажмите кнопку **ОК**. В качестве ИД пакета введите значение, определенное на шаге 3.  

    7.  Нажмите кнопку **Обновить объект**и в области **Свойства** выберите свойство **EnableLabShell** .  

    8.  Щелкните элемент **Изменить свойство**, измените значение на **TRUE**и выберите **Сохранить**.  

    9. Щелкните **Сохранить объект**и закройте тестер инструментария управления Windows.  

10. Прежде чем загрузочный образ можно будет использовать в последовательности задач, его необходимо распространить в точки распространения, группы точек распространения или коллекции, которые связаны с группами точек распространения. Чтобы распространить загрузочный образ, выполните следующие действия.  

    1.  В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.  

    2.  В рабочей области **Библиотека программного обеспечения** разверните узел **Операционные системы**и выберите **Загрузочные образы**.  

    3.  Выберите загрузочный образ, определенный на шаге 3.  

    4.  На вкладке **Главная** в группе **Развертывание** нажмите кнопку **Обновить точки распространения**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Настройка загрузочного образа, использующего среду предустановки Windows 3.1  
 Чтобы настроить загрузочный образ, использующий среду предустановки Windows 3.1, необходимо установить Windows AIK, установить дополнительный компонент Windows AIK для Windows 7 с пакетом обновления 1 (SP1) и использовать программу командной строки DISM для подключения загрузочного образа, добавления дополнительных компонентов и драйверов и фиксации изменений в загрузочном образе. Ниже описана процедура настройки загрузочного образа.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Процедура настройки загрузочного образа, использующего среду предустановки Windows 3.1  

1.  Установите Windows AIK на компьютере, на котором не установлена другая версия Windows AIK или Windows ADK и отсутствуют какие-либо компоненты Configuration Manager. Загрузите Windows AIK из [Центра загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=5753).  

2.  Установите дополнительный компонент Windows AIK для Windows 7 с пакетом обновления 1 (SP1) на компьютере из шага 1. Скачайте дополнительный компонент Windows AIK для Windows 7 с пакетом обновления 1 (SP1) из [Центра загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=5188).  

3.  Скопируйте загрузочный образ (wimpe.wim) из папки установки Windows AIK (например, <*путь_установки*>\Windows AIK\Tools\PETools\amd64\\) в папку на компьютере, с которого будет выполняться настройка загрузочного образа. В этой процедуре в качестве имени папки используется C:\WinPEWAIK.  

4.  Используйте DISM для подключения загрузочного образа к локальной папке среды предустановки Windows. Например, введите следующую команду:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     где C:\WinPEWAIK — папка, содержащая загрузочный образ, а C:\WinPEMount — папка подключения.  

    > [!NOTE]
    >  Дополнительные сведения о DISM см. в статье [Технический справочник по системе обслуживания образов развертывания и управления ими](http://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) в библиотеке документации TechNet по Windows 7.  

5.  После подключения загрузочного образа используйте DISM для добавления в него дополнительных компонентов. Например, в среде предустановки Windows 3.1 дополнительные компоненты находятся в папке <*путь_установки*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

    > [!NOTE]
    >  В этой процедуре используется следующее расположение дополнительных компонентов: C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs. Используемый путь может отличаться в зависимости от версии и параметров установки Windows AIK.  

     Введите следующие команды для установки дополнительных компонентов:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<язык\>* **\winpe-wmi_** *<язык\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<язык\>* **\winpe-scripting_** *<язык\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<язык\>* **\winpe-wds-tools_** *<язык\>* **.cab"**  

     Где C:\WinPEMount — подключенная папка, а языковой стандарт — языковой стандарт для компонентов. Например, для языкового стандарта **en-us** следует ввести:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

    > [!TIP]
    >  Дополнительные сведения о различных пакетах, которые могут быть добавлены в загрузочный образ, см. в статье [Добавление пакета в образ Windows PE](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) в библиотеке документации TechNet по Windows 7.  

6.  Используйте DISM для добавления в загрузочный образ специальных драйверов, если это необходимо. Введите следующую команду для добавления в загрузочный образ драйверов, если это необходимо:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *путь_к_INF-файлу_драйвера* **>**  

     где C:\WinPEMount — папка подключения.  

7.  Введите следующую команду, чтобы отключить файл загрузочного образа и зафиксировать изменения:  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     где C:\WinPEMount — папка подключения.  

8.  Добавьте обновленный загрузочный образ в Configuration Manager, чтобы он стал доступным для использования в последовательностях задач. Чтобы импортировать обновленный загрузочный образ, выполните следующие действия.  

    1.  В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.  

    2.  В рабочей области **Библиотека программного обеспечения** разверните узел **Операционные системы**и выберите **Загрузочные образы**.  

    3.  На вкладке **Главная** в группе **Создать** щелкните элемент **Добавить загрузочный образ** , чтобы запустить мастер добавления загрузочного образа.  

    4.  На странице **Источник данных** настройте следующие параметры, затем нажмите кнопку **Далее**.  

        -   В поле **Путь** укажите путь к обновленному файлу загрузочного образа. Указанный путь должен быть допустимым сетевым путем в формате UNC. Например: **\\\\<***имя_сервера***>\\<***общая папка WinPEWAIK***>\winpe.wim**.  

        -   В раскрывающемся списке **Загрузочный образ** выберите загрузочный образ. Если в WIM-файле содержится несколько загрузочных образов, все они указываются в списке.  

    5.  На странице **Общие** укажите следующие параметры и нажмите кнопку **Далее**.  

        -   В поле **Имя** введите уникальное имя загрузочного образа.  

        -   В поле **Версия** введите номер версии загрузочного образа.  

        -   В поле **Комментарий** введите краткое описание порядка использования загрузочного образа.  

    6.  Завершите работу мастера.  

9. Можно включить в загрузочном образе командную оболочку для его отладки и устранения неполадок в среде предустановки Windows. Чтобы включить командную оболочку, выполните следующие действия.  

    1.  В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.  

    2.  В рабочей области **Библиотека программного обеспечения** разверните узел **Операционные системы**и выберите **Загрузочные образы**.  

    3.  Найдите в списке новый загрузочный образ и определите для него ИД пакета. ИД пакета можно найти в столбце **Идентификатор образа** напротив загрузочного образа.  

    4.  В командной строке введите команду **wbemtest** , чтобы открыть тестер инструментария управления Windows.  

    5.  Введите **\\\\<***компьютер_поставщика_SMS***>\root\sms\site_<***код_сайта***>** в поле **Пространство имен** и нажмите кнопку **Подключить**.  

    6.  Нажмите кнопку **Открыть экземпляр**, введите **sms_bootimagepackage.packageID="<ИД_пакета\>"** и нажмите кнопку **ОК**. В качестве ИД пакета введите значение, определенное на шаге 3.  

    7.  Нажмите кнопку **Обновить объект**и в области **Свойства** выберите свойство **EnableLabShell** .  

    8.  Щелкните элемент **Изменить свойство**, измените значение на **TRUE**и выберите **Сохранить**.  

    9. Щелкните **Сохранить объект**и закройте тестер инструментария управления Windows.  

10. Прежде чем загрузочный образ можно будет использовать в последовательности задач, его необходимо распространить в точки распространения, группы точек распространения или коллекции, которые связаны с группами точек распространения. Чтобы распространить загрузочный образ, выполните следующие действия.  

    1.  В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.  

    2.  В рабочей области **Библиотека программного обеспечения** разверните узел **Операционные системы**и выберите **Загрузочные образы**.  

    3.  Выберите загрузочный образ, определенный на шаге 3.  

    4.  На вкладке **Главная** в группе **Развертывание** нажмите кнопку **Обновить точки распространения**.  
