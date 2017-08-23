---
title: "Управление доступом к службам Office 365 для управляемых компьютеров | Документы Майкрософт"
description: "Сведения о настройке условного доступа для компьютеров, управляемых System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: "15"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: aede531a0406c3d30c9cca957896e002ed22ae51
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Управление доступом к службам Office 365 для компьютеров под управлением System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Начиная с Configuration Manager версии 1602 можно настроить условный доступ для компьютеров, управляемых System Center Configuration Manager.  

> [!IMPORTANT]  
> Эта функция предварительного выпуска доступна в обновлении 1602, 1606 и 1610. Функции предварительной версии включены в продукт для раннего тестирования в рабочей среде, но не следует считать их готовыми к работе. Дополнительные сведения см. в разделе [Использование функций предварительной версии из обновлений](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).
> - После установки обновления 1602 тип компонента отображается как выпущенный, даже если это предварительная версия.
> - При обновлении версии 1602 до 1606 тип компонента отображается как выпущенный, даже если это по-прежнему предварительная версия.
> - При обновлении версии 1511 сразу до 1606 тип компонента отображается как предварительная версия.

Если вам нужны сведения о настройке условного доступа для устройств, зарегистрированных и управляемых Intune, или компьютеров, которые были присоединены к домену и не проверены на соответствие требованиям, ознакомьтесь с разделом [Управление доступом к службам в System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).

## <a name="supported-services"></a>Поддерживаемые службы  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>Поддерживаемые компьютеры  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Поддерживаемые серверы Windows

-   2008 R2
-   2012
-   2012 R2
-   2016

    > [!IMPORTANT]
    > Для серверов Windows, поддерживающих выполнение входа несколькими пользователями одновременно, для всех этих пользователей нужно развернуть те же политики условного доступа.

## <a name="configure-conditional-access"></a>Настройка условного доступа  
 Чтобы настроить условный доступ, необходимо сначала создать политику соответствия требованиям и настроить политику условного доступа. При настройке политик условного доступа для компьютеров можно указать, что компьютеры должны соответствовать политике соответствия требованиям, чтобы получить доступ к службам Exchange Online и SharePoint Online.  

### <a name="prerequisites"></a>Предварительные требования  

-   Синхронизация ADFS и подписка на Office 365. Подписка Office 365 для настройки Exchange Online и SharePoint Online.  

-   Подписка Microsoft Intune. Подписка Microsoft Intune должна быть настроена в консоли Configuration Manager. Подписка Intune используется для передачи состояния соответствия устройства в Azure Active Directory и лицензирования пользователей.  

 Компьютеры должны соответствовать следующим требованиям.  

-   [Необходимые компоненты](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) для автоматической регистрации устройств в Azure Active Directory  

     Можно регистрировать компьютеры с помощью политики соответствия требованиям Azure AD.  

    -   В случае компьютеров под управлением Windows 8.1 и Windows 10 можно использовать групповую политику Active Directory, чтобы настроить устройства для автоматической регистрации в Azure AD.  

    -   o Для компьютеров под управлением Windows 7 необходимо развернуть пакет программного обеспечения для регистрации устройств на компьютере Windows 7 с помощью System Center Configuration Manager. Дополнительные сведения приведены в разделе [Автоматическая регистрация в Azure Active Directory присоединенных к домену устройств Windows](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   Необходимо использовать Office 2013 или Office 2016 с [включенной](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)современной проверкой подлинности.  

 Описанные ниже действия применимы к Exchange Online и SharePoint Online.  

### <a name="step-1-configure-compliance-policy"></a>Шаг 1. Настройка политики соответствия требованиям  
 В консоли Configuration Manager создайте политику соответствия требованиям со следующими правилами.  

-   Требовать регистрацию в Azure Active Directory — это правило проверяет, присоединено ли устройство пользователя к Azure AD. Если нет, устройство автоматически регистрируется в Azure AD. Автоматическая регистрация поддерживается только в Windows 8.1. Для ПК Windows 7 разверните MSI-файл, выполняющий автоматическую регистрацию. Дополнительные сведения см. в статье [Автоматическая регистрация в Azure Active Directory присоединенных к домену устройств Windows](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   **Установка всех обязательных обновлений с крайним сроком старше определенного числа дней** — это правило проверяет, установлены ли на устройстве пользователя все необходимые обновления (указанные в правиле "Обязательные автоматические обновления") в срок и в течение указанного льготного периода, и автоматически устанавливает все отложенные обязательные обновления.  

-   **Требовать шифрование диска BitLocker** — это правило проверяет, зашифрован ли основной диск (например, C:\\) на устройстве с помощью BitLocker. Если шифрование Bitlocker не включено на основном устройстве, доступ к электронной почте и службам SharePoint блокируется.  

-   **Требовать защиту от вредоносных программ** — это правило проверяет, включено ли и выполняется ли программное обеспечение по защите от вредоносных программ (System Center Endpoint Protection или только Защитник Windows). Если ПО не включено, доступ к электронной почте и службам SharePoint блокируется.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Шаг 2. Оценка влияния условного доступа  
 Выполните отчет о соответствии условного доступа. Его можно найти в разделе "Мониторинг", выбрав "Отчеты" > "Управление соответствием и параметрами". В нем отображено состояние соответствия требованиям для всех устройств.  Устройствам, которые будут определены как несоответствующие требованиям, доступ к Exchange Online и SharePoint Online будет заблокирован.  

 ![CA&#95;compliance&#95;report](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Настройка групп безопасности Active Directory  
 Политики условного доступа нацеливаются на группы пользователей, в соответствии с типами политик. Эти группы содержат пользователей, которые будут являться целями для политики или будут исключены из нее. Когда пользователь попадает под действие политики, каждое используемое им устройство должно соответствовать требованиям, чтобы получить доступ к службе.  

 Группы безопасности Active Directory. Эти группы пользователей должны быть синхронизированы с Azure Active Directory. Кроме того, эти группы можно настроить в Центре администрирования Office 365 или на портале учетных записей Intune.  

 В каждой политике можно указать два типа групп. :  

-   **Целевые группы** — группы пользователей, к которым применяется данная политика. Для политики соответствия требованиям и политики условного доступа следует использовать одну и ту же группу.  

-   **Исключенные группы** — группы пользователей, которые исключены из политики (необязательно).  
    Если пользователь входит в обе группы, то он будет исключен из политики.  

     Оценка производится только для тех групп, которые являются целевыми для политики условного доступа.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Шаг 3.  Создание политики условного доступа для Exchange Online и SharePoint Online  

1.  В консоли Configuration Manager щелкните элемент **Активы и соответствие**.  

2.  Чтобы создать политику для Exchange Online, щелкните **Включить политику условного доступа для Exchange Online**.  

     Чтобы создать политику для SharePoint Online, щелкните **Включить политику условного доступа для SharePoint Online**.  

3.  На вкладке **Главная** в группе **Ссылки** щелкните пункт **Настройка политики условного доступа в консоли Intune**. Может потребоваться ввести имя пользователя и пароль учетной записи, используемой для подключения Configuration Manager к Intune.  

     Откроется консоль администрирования Intune.  

4.  Для Exchange Online: в консоли администрирования Microsoft Intune щелкните **Политика > Условный доступ > Политика Exchange Online**.  

     Для SharePoint Online: в консоли администрирования Microsoft Intune щелкните **Политика > Условный доступ > Политика SharePoint Online**.  

5.  Выберите параметр**Устройства должны соответствовать требованиям**, чтобы задать требование для компьютеров Windows.  

6.  В разделе **Целевые группы**щелкните **Изменить**, чтобы выбрать группы безопасности Azure Active Directory, к которым будет применена политика.  

    > [!NOTE]  
    >  Для развертывания политики соответствия требованиям и политики условного доступа следует использовать одну и ту же целевую группу безопасности.  

     Дополнительно в разделе **Исключенные группы**можно щелкнуть **Изменить**, чтобы выбрать группы безопасности Azure Active Directory, которые будут исключены из этой политики.  

7.  Щелкните **Сохранить**, чтобы создать и сохранить политику.  

 Пользователи, заблокированные из-за несоответствия требованиям, смогут просматривать сведения о соответствии в центре программного обеспечения Configuration Manager и запускать новые оценки политики после устранения проблем соответствия.  

<!---
##  <a name="bkmk_KnownIssues"></a> Known issues  
 You may see the following issues when using this feature:  

-   In this 1602 update,  the 5 day compliance is not enforced. Even if compliance check on the end-user's device has happened more than 5 days ago, users still can access Office 365 and SharePoint online.  

-   When a device is not compliant with the compliance policy, the reason is not automatically displayed. The end- user must go to the new Software Center to find the reason for non-compliance. The reason is displayed in the Device compliance section of the Software Center.  

-   Windows 10 users may see multiple access failures when trying to reach O365 and/or SharePoint online resources. Note that conditional access is not fully supported for Windows 10.  
--->
## <a name="see-also"></a>См. также

- [Защита данных и инфраструктуры сайтов с помощью System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Conditional access troubleshooting flow-chart for Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0) (Схема устранения неполадок условного доступа для Configuration Manager)
