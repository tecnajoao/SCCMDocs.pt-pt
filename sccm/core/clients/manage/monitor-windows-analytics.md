---
title: "Мониторинг клиентов — использование Windows Analytics совместно с Configuration Manager | Документация Майкрософт"
description: "Windows Analytics — это набор решений, работающих под управлением Operations Management Suite, которые предоставляют ценные сведения о текущем состоянии среды на основе данных телеметрии Windows, полученных от размещенных в этой среде устройств."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Использование Windows Analytics совместно с Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) — это набор решений, которые работают под управлением [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview). Эти решения предоставляют сведения о текущем состоянии среды. Устройства в вашей среде передают данные телеметрии Windows. Эти данные можно просматривать и анализировать с помощью решений на веб-портале [Operations Management Suite](https://mms.microsoft.com). Если вы используете решение [Проверка готовности к обновлению](/sccm/core/clients/manage/upgrade/upgrade-analytics), данные можно использовать еще и в узле мониторинга в консоли Configuration Manager, если это решение к Configuration Manager.

Данные телеметрии Windows, используемые в Windows Analytics, не передаются напрямую на сервер сайта Configuration Manager. Клиентские компьютеры отправляют данные телеметрии Windows через службу телеметрии. Затем необходимые данные передаются в аналитические решения Windows, размещенные в одной из рабочих областей OMS, используемых в организации. Configuration Manager может предоставить вам на веб-портале контекстные ссылки на соответствующие данные или отобразить эти данные напрямую, если они являются частью решений, подключенных к Configuration Manager. Также вы можете напрямую обращаться к данным через веб-портал Operation Management Suite.

>[!Important]
>[Данные Configuration Manager по диагностике и использованию](../../plan-design/diagnostics/diagnostics-and-usage-data.md), которые передаются в корпорацию Майкрософт с сервера сайта Configuration Manager, никак не связаны с Windows Analytics и телеметрией Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Настройка клиентов для передачи данных в Windows Analytics

Чтобы клиентские устройства передавали данные в Windows Analytics, каждому из них необходимо предоставить ключ коммерческого идентификатора, связанный с рабочей областью Operations Management Suite, в которой размещается Windows Analytics для вашей организации. Также для устройств нужно настроить уровень данных телеметрии, соответствующий конкретному решению или решениям, которые вы хотите использовать. 

### <a name="configure-windows-analytics-client-settings"></a>Настройка параметров клиента Windows Analytics
Чтобы настроить Windows Analytics, в консоли Configuration Manager выберите пункт **Администрирование** > **Параметры клиента**, дважды щелкните элемент **Создать пользовательские параметры клиента устройства** и выберите **Windows Analytics**.  

Затем перейдите к вкладке с параметрами **Windows Analytics** и настройте следующее:
  -  **Коммерческий идентификатор**  
Ключ коммерческого идентификатора сопоставляет сведения с управляемых устройств с рабочей областью OMS, в которой размещаются корпоративные данные Windows Analytics. Если вы уже настроили ключ коммерческого идентификатора для использования с функцией проверки готовности к обновлению, выберите его. Если у вас еще нет ключа коммерческого идентификатора, см. инструкции по [его созданию]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Уровень телеметрии для устройств Windows 10**   
Сведения о том, какие данные собираются на каждом уровне телеметрии Windows 10, см. в статье о [настройке телеметрии Windows в организации](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

  -  **Согласие на сбор коммерческих данных на устройствах под управлением Windows 7, 8 и 8.1**   
Сведения о данных, собираемых в этих операционных системах после вашего согласия, см. в PDF-файле [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Поля и события по оценке телеметрии для Windows 7, Windows 8 и Windows 8.1) от корпорации Майкрософт.

  -  **Настройка сбора данных Internet Explore**  
На устройствах под управлением Windows 8.1 или более ранних версий вы можете разрешить сбор данных в Internet Explorer, который позволит решению "Проверка готовности к обновлению" выявить несовместимости веб-приложений, которые могут помешать обновлению до Windows 10. Сбор данных Internet Explorer можно включить для каждой зоны Интернета. Дополнительные сведения о зонах Интернета см. в статье [о зонах безопасности URL-адресов](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Использование решения "Проверка готовности к обновлению" для выявления проблем совместимости с Windows 10

Решение "Проверка готовности к обновлению" (ранее называлось Upgrade Analytics) позволяет анализировать готовность устройства и его совместимость с Windows 10. Эта оценка помогает избежать проблем при обновлении Когда вы подключите Configuration Manager к решению "Проверка готовности к обновлению", данные о совместимости будут передаваться прямо в консоль Configuration Manager. После этого вы сможете назначать устройства из списка устройств для обновления или исправления.

Дополнительные сведения и сведения о настройке и подключении этих систем см. в руководстве по [интеграции решения "Проверка готовности к обновлению" с System Center Configuration Manager](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Использование Windows Analytics для выявления недостатков в политиках Windows Information Protection

Устройства под управлением Windows 10 версии 1703 или более поздней, для которых настроена политика [Windows Information Protection](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP), передают данные телеметрии о приложениях, имеющих доступ к корпоративным данным в вашей среде, но не учтенных в правилах применения политики WIP. Возможно, эти приложения нужны пользователям вашей среды для эффективного выполнения своих задач, но доступ для них заблокирован. Понимание того, что этим приложениям нужен доступ к корпоративным данным, будет полезным при обслуживании политик Windows Information Protection в Configuration Manager. 

Эти данные Windows Information Protection можно получить с помощью [запроса Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).