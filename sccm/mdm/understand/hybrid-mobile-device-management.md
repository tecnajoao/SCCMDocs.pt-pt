---
title: MDM híbrida com o Microsoft Intune
titleSuffix: Configuration Manager
description: Saiba mais sobre a gestão de dispositivos móveis (MDM) híbrida com o Configuration Manager e o Microsoft Intune.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2980cef8a39f790dbb94ab85fa025eeb04f4f996
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139294"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>MDM híbrida com o Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). A partir da versão de serviço de Intune 1902, era esperada no final de Fevereiro de 2019, novos clientes não é possível criar uma nova ligação híbrida. 
> <!--Intune feature 2683117-->  
> Desde a iniciar-se no Azure ao longo de um ano atrás, o Intune adicionou centenas de novas funções do serviço solicitados pelo cliente e líder do mercado. Agora, ele oferece recursos muito mais do que os oferecidos por gestão de dispositivos móveis híbridos (MDM). O Intune no Azure fornece uma experiência administrativa mais integrada e otimizada para as suas necessidades de mobilidade empresarial.
> 
> Como resultado, a maioria dos clientes escolher o Intune no Azure através de hybrid MDM. O número de clientes que utilizam a MDM híbrida continua a diminuir quando mais clientes mover para a cloud. Por conseguinte, 1 de Setembro de 2019 Microsoft irão extinguir a oferta de serviço MDM híbrida. Tenha em conta suas [migração para o Intune no Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) para suas necessidades de MDM. 
> 
> Esta alteração não afeta o Gestor de configuração no local ou [cogestão para dispositivos Windows 10](/sccm/comanage/overview). Se tiver certeza se estiver a utilizar o MDM híbrida, avance para o **Administration** área de trabalho da consola do Configuration Manager, expanda **serviços Cloud**e clique em **Microsoft Intune Subscrições**. Se tiver uma subscrição do Microsoft Intune configurado, o seu inquilino estiver configurado para híbrida MDM.
> 
> **Como isto me afeta?**
> 
> - Microsoft irá suportar seu híbrido utilização MDM para o próximo ano. A funcionalidade irá continuar a receber correções de erros importantes. Microsoft irá suportar a funcionalidade existente em novas versões de SO, por exemplo, a inscrição em dispositivos iOS 12. Não haverá nenhuma novas funcionalidades para hybrid MDM.  
> 
> - Se migrar para o Intune no Azure antes do final da oferta de MDM híbrida, não deverá haver nenhum impacto no utilizador final.  
> 
> - 1 de Setembro de 2019, quaisquer dispositivos MDM híbrida restantes não receberão mais política, as aplicações ou atualizações de segurança.  
> 
> - Licenciamento permanece igual. Intune no licenças do Azure estão incluídas com a MDM híbrida  
> 
> - A funcionalidade MDM no local no Configuration Manager não está a ser preterida. A partir do Configuration Manager versão 1810, pode utilizar o MDM no local sem uma ligação do Intune. Para obter mais informações, consulte [Intune de uma ligação já não é necessária para novas implementações de MDM no local](/sccm/core/plan-design/changes/whats-new-in-version-1810#bkmk_opmdm). 
> 
> - A funcionalidade de acesso condicional no local do Configuration Manager também é preterida híbrido MDM. Se utilizar o acesso condicional em dispositivos geridos com o cliente do Configuration Manager, certifique-se de que estão protegidos antes de migrar. 
>     1. Definir políticas de acesso condicional no Azure
>     2. Configurar políticas de conformidade no portal do Intune 
>     3. Concluir migração híbrida e defina a autoridade de MDM ao Intune
>     4. Ativar a cogestão
>     5. Mover a carga de trabalho de cogestão de políticas de conformidade para o Intune 
>
>     Para obter mais informações, consulte [acesso condicional com cogestão](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 
> 
> **O que preciso fazer para se preparar para esta alteração?**
> 
> - Começar a planejar sua migração da MDM a partir da consola do ConfigMgr para o Azure. Muitos clientes, incluindo o Microsoft IT, já leu este processo. Para obter mais informações, consulte esta [estudo de caso da Microsoft](https://aka.ms/Intune_MSFT).  
> 
> - Reveja as seguintes ferramentas e documentação para simplificar o processo de transferência da MDM híbrida para o Intune no Azure:  
>     - [Importar os dados do Configuration Manager para o Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>     - [Migrar os utilizadores e dispositivos da MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
> 
> - Contacte o seu parceiro de registo ou FastTrack para obter assistência. [O FastTrack para Microsoft 365](https://aka.ms/hybrid_fasttrack) pode auxiliar na migração da MDM híbrida para o Intune no Azure. 
> 
> Para obter mais informações, consulte [a mensagem de blogue de suporte do Intune](https://aka.ms/hybrid_notification).



Com a híbrida dispositivos móveis (MDM) funcionalidade de gestão do Configuration Manager, gerir dispositivos Android, iOS e Windows. Todas as tarefas de gestão são tratadas da consola do Configuration Manager, onde realizar o restante de suas tarefas de gestão integrada diretamente ao serviço online Microsoft Intune através da internet. Utilize o Gestor de configuração para permitir que os utilizadores aceder a recursos da empresa nos respetivos dispositivos de forma segura e gerida. Ao utilizar a gestão de dispositivos, é possível proteger dados da empresa, permitindo que os utilizadores inscrevam os respetivos dispositivos pessoais ou pertencentes à empresa aos dados da empresa. 

Este artigo pressupõe que utiliza o Configuration Manager para gerir computadores. Também parte do princípio que está interessado em expandir a consola do Configuration Manager com o Intune para gerir dispositivos móveis. 



## <a name="capabilities"></a>Funções

MDM híbrida suporta as seguintes capacidades de gestão nos dispositivos:

-   Extinguir e apagar dispositivos  

-   Configurar as definições de compatibilidade como palavras-passe, segurança, roaming, encriptação e comunicação wireless  

-   Implementar aplicações de linha de negócio (LOB) em dispositivos  

-   Implementar aplicações em dispositivos que se liguem à Windows Store, à Loja do Windows Phone, à App Store ou Google Play  

-   Recolher inventário de hardware  

-   Recolher inventário de software ao utilizar relatórios incorporados  

Para ler sobre que novas funcionalidades estão disponíveis para MDM híbrida, veja [quais são as novidades na gestão de dispositivos móveis híbrida](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management).



## <a name="hybrid-mdm-enrollment"></a>Inscrição de MDM híbrida

Para trazer dispositivos para gestão híbrida, esses dispositivos têm de estar inscritos com o serviço. Como os dispositivos inscrevem dispositivos depende do tipo de dispositivo, da propriedade e o nível de gestão necessário.

- **"Bring your own device" (BYOD)**: Os utilizadores inscrevem os respetivos pessoais telemóveis, tablets ou PCs  

- **Dispositivo pertencente à empresa (COD)**: Ativar cenários de gestão como eliminação remota, dispositivos partilhados ou afinidade de utilizador para um dispositivo  

- Se usar [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), no local ou alojado na cloud, pode ativar a gestão simples do Intune sem inscrição. Windows PCs também podem ser geridos com [software de cliente Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
