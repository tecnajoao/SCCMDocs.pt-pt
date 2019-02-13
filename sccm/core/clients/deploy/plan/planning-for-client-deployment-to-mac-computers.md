---
title: Planear a implementação de cliente para computadores Mac
titleSuffix: Configuration Manager
description: Plano de implementação do cliente em computadores Mac no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe9c5a22f1c3a17737ccfb452b3cd4dd418bf9a9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142464"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-system-center-configuration-manager"></a>Planear a implementação do cliente em computadores Mac no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode instalar o cliente do Configuration Manager em computadores Mac que executam o sistema de operativo Mac OS X e utilizam as seguintes capacidades de gestão:  

- **Inventário de hardware**  

   Pode utilizar o inventário de hardware do Configuration Manager para recolher informações sobre o hardware e aplicativos instalados em computadores Mac. Estas informações podem ser visualizadas no Explorador de recursos na consola do Configuration Manager e utilizadas para criar coleções, consultas e relatórios. Para obter mais informações, consulte [como utilizar o Explorador de recursos para ver o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   O Configuration Manager recolhe as seguintes informações de hardware de computadores Mac:  

  -   Processador  

  -   Sistema de computador  

  -   Unidade de disco  

  -   Partição de disco  

  -   Placa de rede  

  -   Sistema operativo  

  -   Serviço  

  -   Processo  

  -   Software instalado  

  -   Produto de sistema do computador  

  -   Controlador USB  

  -   Dispositivo USB  

  -   Unidade de CD-ROM  

  -   Controlador de vídeo  

  -   Monitor de secretária  

  -   Bateria portátil  

  -   Memória física  

  -   Impressora  

  > [!IMPORTANT]  
  >  Não é possível expandir as informações de hardware que são recolhidas de computadores Mac durante o inventário de hardware.  

- **Definições de compatibilidade**  

   Pode utilizar as definições de compatibilidade do Configuration Manager para ver a conformidade das e remediar as definições do Mac OS X (. plist). Por exemplo, pode impor definições para a home page do browser Safari ou certifique-se de que a firewall Apple está ativada. Também pode utilizar scripts de shell para monitorizar e remediar as definições no MAC OS X.  

- **Gestão de aplicações**  

   O Configuration Manager pode implementar software em computadores Mac. Pode implementar os seguintes formatos de software para computadores Mac:  

  -   Imagem de disco Apple (. DMG)  

  -   Ficheiro de pacote meta (. MPKG)  

  -   Pacote de instalador dos X do Mac (. PKG)  

  -   Aplicação do Mac OS X (. APLICAÇÃO)  

  Quando instala o cliente do Configuration Manager em computadores Mac, não é possível utilizar as seguintes capacidades de gestão que são suportadas pelo cliente do Configuration Manager em computadores baseados no Windows:  

- Instalação push do cliente  

- Implementação do sistema operativo  

- Atualizações de software  

  > [!NOTE]  
  >  Pode utilizar a gestão de aplicações do Configuration Manager para implementar atualizações de software necessárias do Mac OS X em computadores Mac. Além disso, pode utilizar as definições de compatibilidade para se certificar de que os computadores têm todas as atualizações de software necessárias.  

- Janelas de manutenção  

- Controlo remoto  

- Gestão de energia  

- Verificação de cliente do estado do cliente e remediação  

  Para obter mais informações sobre como instalar e configurar o cliente do Configuration Manager Mac, consulte [como implementar clientes em Macs no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md).
