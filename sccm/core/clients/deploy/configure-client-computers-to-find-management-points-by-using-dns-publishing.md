---
title: "Настройка клиентов для поиска точек управления с использованием публикации DNS | Документы Майкрософт"
description: "Настройка клиентских компьютеров на поиск точек управления с использованием публикации DNS в System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d016ec3fe106b2d90b3c14b4f9296aed4d198644
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>Настройка клиентских компьютеров на поиск точек управления с использованием публикации DNS в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Чтобы оставаться управляемыми, клиенты в System Center Configuration Manager должны находить точку управления для выполнения назначения сайтов и далее выполнять это действие на постоянной основе. Доменные службы Active Directory предоставляют клиентам наиболее безопасный способ поиска точек управления в интрасети. Однако если клиенты не могут использовать этот метод поиска служб (например, если схема Active Directory не была расширена или если клиенты находятся в рабочей группе), в качестве предпочтительного метода поиска служб следует использовать публикацию DNS.  

> [!NOTE]  
>  При установке клиента для Linux и UNIX необходимо указать точку управления для использования в качестве начальной точки контакта. Сведения об установке клиента для Linux и UNIX см. в статье [Развертывание клиентов на серверах UNIX и Linux в System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Перед использованием публикации DNS для точек управления следует убедиться в том, что серверы DNS в интрасети имеют записи ресурса нахождения службы (SRV RR) и соответствующие записи ресурса узла (A или AAA) для точек управления сайта. Записи ресурса нахождения службы могут создаваться автоматически Configuration Manager или вручную администратором DNS, создающим записи в DNS.  

 Дополнительные сведения о публикации DNS как методе обнаружения служб для клиентов Configuration Manager см. в статье [Пояснения о том, как клиенты находят ресурсы и службы сайта для System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 По умолчанию клиенты ищут точки управления DNS в своем домене DNS. Однако если опубликованных точек управления в домене клиентов нет, необходимо вручную настроить клиенты с суффиксом DNS точки управления. Настроить этот суффикс DNS на клиентах можно во время или после установки клиента:  

-   Чтобы настроить клиенты для суффикса точки управления во время установки клиента, настройте свойства CCMSetup Client.msi.  

-   Чтобы настроить на клиентах суффикс точек управления после установки клиентов, откройте панель управления и настройте **Свойства Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Настройка на клиентах суффикса точек управления во время установки клиента  

-   Установите клиент с использованием следующего свойства CCMSetup Client.msi:  

    -   **DNSSUFFIX=** *&lt;домен точки управления\>*  

         Если у сайта несколько точек управления, и они находятся в различных доменах, укажите только один домен. При подключении к точке управления в этом домене клиент загрузит список доступных точек управления, включая точки управления из других доменов.  

     Дополнительные сведения о свойствах командной стройки CCMSetup см. в статье [О свойствах установки клиента в Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Настройка на клиентах суффикса точек управления после установки клиента  

1.  В панели управления клиентского компьютера перейдите к пункту **Configuration Manager**и дважды щелкните **Свойства**.  

2.  На вкладке **Сайт** укажите DNS-суффикс точки управления, после чего нажмите кнопку **ОК**.  

     Если у сайта несколько точек управления, и они находятся в различных доменах, укажите только один домен. При подключении к точке управления в этом домене клиент загрузит список доступных точек управления, включая точки управления из других доменов.
