---
title: "Синхронизация данных | Документы Майкрософт | Microsoft Operations Management Suite "
description: "Синхронизация данных System Center Configuration Manager с Microsoft Operations Management Suite."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 608a9893011c6500d5d4cd2f756a124db66b1858
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Синхронизация данных Configuration Manager с Microsoft Operations Management Suite

*Применимо к: System Center Configuration Manager (Current Branch)*

Вы можете использовать **мастер служб Azure** для настройки подключения Configuration Manager к облачной службе Operations Management Suite (OMS). Начиная с версии 1706 мастер заменяет собой все рабочие процессы, которые раньше использовались для настройки этого подключения. Если вы используете предыдущие версии, см. раздел о [синхронизации данных Configuration Manager с Microsoft Operations Management Suite (версия 1702 и предыдущие)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

-   Мастер позволяет настраивать облачные службы для Configuration Manager, например OMS, Магазин Windows для бизнеса и Azure Active Directory.  

-   Configuration Manager использует такие функции OMS, как [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) и [Проверка готовности к обновлению](/sccm/core/clients/manage/upgrade/upgrade-analytics).

## <a name="prerequisites-for-the-oms-connector"></a>Предварительные требования для использования соединителя OMS
Предварительные требования для настройки подключения к OMS не отличаются от тех, которые [описаны для версии Current Branch 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Здесь мы перечислим их снова.  

-   Перед установкой соединителя OMS в Configuration Manager, необходимо предоставить Configuration Manager разрешения для доступа к OMS. Это должны быть *права участника* для *группы ресурсов* Azure, в которой содержится рабочая область OMS Log Analytics. Процедура предоставления прав описана в содержимом Log Analytics. См. раздел [Предоставление Configuration Manager разрешений в OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) в документации OMS.

-   Соединитель OMS следует устанавливать на компьютере, на котором размещается [точка подключения службы](/sccm/core/servers/deploy/configure/about-the-service-connection-point) в [оперативном режиме](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Вместе с соединителем OMS в точке подключения службы необходимо установить Microsoft Monitoring Agent для OMS. Агент мониторинга и соединитель OMS должны быть настроены на использование одной **рабочей области OMS**. Процесс установки агента описан в разделе [Загрузка и установка агента](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) документации OMS.
-   Когда вы завершите установку соединителя и агента, следует настроить OMS для использования данных Configuration Manager. Для этого [импортируйте коллекции Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections) на портале OMS.

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Использование мастера служб Azure для настройки подключения к OMS

1.  В консоли последовательно выберите **Администрирование** > **Обзор** > **Облачные службы** > **Службы Azure** и щелкните **Настроить службы Azure** на вкладке ленты **Главная**, чтобы запустить **Мастер служб Azure**.

2.  На странице **Службы Azure** выберите облачную службу Operation Management Suite. Введите понятное имя в поле **Имя службы Azure** и необязательное описание, а затем нажмите кнопку **Далее**.

3.  На странице **Приложение** укажите среду Azure (ознакомительная техническая версия поддерживает только общедоступное облако). Нажмите кнопку **Обзор**, чтобы открыть окно приложения сервера.

4.  Выберите веб-приложение.

    -   **Импорт**: чтобы использовать веб-приложение, которое уже существует в вашей подписке Azure, щелкните **Импорт**. Введите понятное имя для приложения и клиента, а затем укажите идентификаторы клиента и секретный ключ для веб-приложения Azure, которые должен использовать Configuration Manager. **Проверив** сведения, нажмите кнопку **ОК** для продолжения.   

    > [!NOTE]   
    > Когда вы настраиваете OMS в этой предварительной версии, OMS поддерживает для веб-приложения только функцию *Импорт*. Создание веб-приложений не поддерживается. Также вы не сможете использовать для OMS уже существующие приложения.

5.  Когда вы выполните все процедуры, на этой странице автоматически отобразятся все сведения из раздела **Настройка подключения к OMS**. Здесь вы должны увидеть сведения о подключении для **подписки Azure**, **группы ресурсов Azure** и **рабочей области Operations Management Suite**.

6.  Мастер подключится к службе OMS, используя указанные вами сведения. Выберите коллекции устройств, которые хотите синхронизировать с OMS, и нажмите кнопку **добавить**.

7.  Проверьте параметры подключения на экране **Сводка**, а затем выберите **Далее**. На экране **Выполняется** отобразится состояние подключения, которое затем изменится на **Завершено**.

8.  Когда мастер завершит работу, в консоли Configuration Manager будет указано, что вы настроили **Operation Management Suite** как **Тип облачной службы**.

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>Синхронизация данных Configuration Manager с Microsoft Operations Management Suite (версия 1702 и предыдущие)


*Применимо к: System Center Configuration Manager (версия 1702 и предыдущие)*

Соединитель Microsoft Operations Management Suite (OMS) можно использовать для синхронизации данных, таких как коллекции, между System Center Configuration Manager и OMS Log Analytics в Microsoft Azure. При этом данные из развертывания Configuration Manager отображаются в OMS.
> [!TIP]
> Соединитель OMS является функцией предварительной версии. Дополнительные сведения см. в статье [Использование функций предварительной версии из обновлений](/sccm/core/servers/manage/pre-release-features).

Начиная с версии 1702 вы можете использовать соединитель OMS для подключения к рабочей области OMS, расположенной в облаке Microsoft Azure для государственных организаций. Для этого перед установкой соединителя OMS нужно изменить файл конфигурации. Подробнее см. раздел [Использование соединителя OMS для облака Azure для государственных организаций](#fairfaxconfig) в этой статье.

### <a name="prerequisites"></a>Предварительные требования
- Перед установкой соединителя OMS в Configuration Manager, необходимо предоставить Configuration Manager разрешения для доступа к OMS. Это должны быть *права участника* для *группы ресурсов* Azure, в которой содержится рабочая область OMS Log Analytics. Процедура предоставления прав описана в содержимом Log Analytics. См. раздел [Предоставление Configuration Manager разрешений в OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) в документации OMS.

- Соединитель OMS следует устанавливать на компьютере, на котором размещается [точка подключения службы](/sccm/core/servers/deploy/configure/about-the-service-connection-point) в [оперативном режиме](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Если вы подключили OMS к автономному первичному сайту и планируете добавить в среду сайт центра администрирования, следует удалить текущее подключение и заново настроить соединитель на новом сайте центра администрирования.

- Вместе с соединителем OMS в точке подключения службы необходимо установить Microsoft Monitoring Agent для OMS.  Агент мониторинга и соединитель OMS должны быть настроены на использование одной **рабочей области OMS**. Процесс установки агента описан в разделе [Загрузка и установка агента](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) документации OMS.

- Когда вы завершите установку соединителя и агента, следует настроить OMS для использования данных Configuration Manager.  Для этого [импортируйте коллекции Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections) на портале OMS.



### <a name="install-the-oms-connector"></a>Установка соединителя OMS  
1. В консоли на портале OMS настройте [иерархию для использования функций предварительной версии](/sccm/core/servers/manage/pre-release-features) и включите использование соединителя OMS.  

2. Теперь перейдите к разделу **Администрирование** > **Облачные службы** > **Соединитель OMS**. На ленте щелкните "Создать подключение к Operations Management Suite". Откроется **мастер подключения к Operations Management Suite**. Выберите **Далее**.  


3.  На экране **Общие** убедитесь, что указаны следующие сведения, и выберите **Далее**.  
  - Configuration Manager зарегистрирован как средство управления "Веб-приложение и/или веб-API" и имеется [идентификатор клиента, полученный при регистрации](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - В Azure Active Directory создан ключ клиента для зарегистрированного средства управления.  

  - На портале управления Azure указано зарегистрированное веб-приложение с разрешением на доступ к OMS, как описано в разделе [Предоставление Configuration Manager разрешений для OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.  На странице **Azure Active Directory** настройте параметры подключения к OMS, указав **клиент**, **идентификатор клиента** и **секретный ключ клиента**, а затем выберите **Далее**.  

5.  На странице **Конфигурация подключения к OMS** укажите параметры подключения, заполнив поля **Подписка Azure**, **Группа ресурсов Azure** и **Рабочая область Operations Management Suite**.  Необходимо использовать ту же рабочую область, которая указана для агента управления Майкрософт, установленного на точке подключения службы.  

6.  Проверьте параметры подключения на странице **Сводка**, а затем выберите **Далее**. На странице **Ход выполнения** будет отображено состояние подключения, а затем появится сообщение **Завершено**.

После связывания OMS с Configuration Manager можно добавлять и удалять коллекции и просматривать свойства подключения OMS.

### <a name="verify-the-oms-connector-properties"></a>Проверка свойств соединителя OMS
1.  В консоли Configuration Manager перейдите в раздел **Администрирование** > **Облачные службы**, а затем выберите **Соединитель OMS**, чтобы открыть страницу **Подключение OMS****.
2.  На этой странице есть две вкладки.
  - **Azure Active Directory.**   
    На этой вкладке отображаются сведения о **клиенте**, **идентификаторе клиента** и **сроке действия секретного ключа клиента**. Здесь можно проверить, завершился ли срок действия секретного ключа клиента.

  - **Свойства соединения OMS.**  
    На этой вкладке отображаются сведения о **подписке Azure**, **группе ресурсов Azure** и **рабочей области Operations Management Suite**, а также список **коллекций устройств, для которых Operations Management Suite может получать данные**. С помощью кнопок **Добавить** и **Удалить** можно указать разрешенные коллекции.

### <a name="fairfaxconfig"> </a> Использование соединителя OMS для облака Azure для государственных организаций


1.  На любом компьютере, на котором установлена консоль Configuration Manager, измените следующий файл конфигурации так, чтобы он указывал на облако для государственных организаций:  ***&lt;путь_установки_Configuration_Manager>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Изменения:**

    Измените значение параметра *FairFaxArmResourceID* на "https://management.usgovcloudapi.net/"

   - **Исходный параметр:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Параметр после изменения:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Измените значение параметра *FairFaxAuthorityResource* на "https://login.microsoftonline.com/"

  - **Исходный параметр:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Измененный параметр:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.  Сохранив файл с внесенными изменениями, перезапустите консоль Configuration Manager на этом же компьютере, а затем установите соединитель OMS с ее помощью. Чтобы установить соединитель, используйте сведения из раздела [Синхронизация данных Configuration Manager с Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) и выберите **рабочую область Operations Management Suite** в облаке Microsoft Azure для государственных организаций.

3.  После установки соединителя OMS подключение к облаку для государственных организаций будет доступно при использовании консоли, подключенной к сайту.
