---
title: Configurar o Azure AD híbrido
titleSuffix: Configuration Manager
description: Se o seu ambiente tem atualmente a dispositivos associados a domínios do Windows 10, configurar híbrida do Azure AD antes de ativar a cogestão
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec02f740485d3f8b466cde0a644aaaa8885b91f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120961"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurar híbrida do Azure AD para a cogestão

Se tiver dispositivos Windows 10 associados ao Active Directory no local, antes de ativar a cogestão no Configuration Manager, associe primeiro estes dispositivos ao Azure Active Directory (Azure AD). Este processo é chamado de associação do Azure AD híbrido. 

No vídeo seguinte, Sandeep Deo do gerente de programas sênior e gerente de marketing de produtos Adam Harbour discutam e demonstrar a configuração de dispositivos no Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

O híbrido do Azure AD join processar automaticamente registra seus dispositivos associados a um domínio de no local com o Azure AD. Para obter mais informações sobre este processo, consulte os artigos seguintes:
- [Introdução à gestão de dispositivos no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Como planear a sua associação do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Associação do híbrida do Azure AD é um dos alicerces chave para a cogestão. Este processo pode ser um desafio para alguns clientes, por exemplo:
- Sua organização utiliza uma solução de identidade de terceiros 
- As complexidades de configuração de segurança de serviços de Federação de diretório Active Directory (ADFS)

Resolver esses desafios, pode demorar algumas orientações. Este artigo ajuda a mitigar quaisquer atrasos.


## <a name="how-to-do-it"></a>Como fazê-lo

Os dispositivos são semelhantes aos utilizadores durante a criação de uma identidade que pretende proteger. Para proteger a identidade de um dispositivo em qualquer altura e em qualquer local, terá de colocar a identidade do que o dispositivo com o Azure AD.

Com base no tipo de domínio que está a utilizar, existem duas formas principais de fazer isso. Configure a associação do Azure AD híbrido para um dos seguintes tipos de domínio:  
- [Domínios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domínios geridos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Os dois métodos anteriores proporcionam a melhor experiência. Para informações mais detalhadas, incluindo o processo totalmente manual, consulte os artigos seguintes:
- [Configurar manualmente os dispositivos de associados ao Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Autenticação pass-through do ADFS para o Azure AD híbrido](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), que inclui a deteção do Azure AD  

Para obter orientações de resolução de problemas, consulte a [associação do Azure AD híbrido com o Windows 10 guia de resolução de problemas](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Estudo de caso

Uma empresa de grande software europeus com mais de 100.000 utilizadores na sua rede ADOTOU uma abordagem faseada e granular para ativar a associação ao Azure AD híbrido.

Durante a fase de planejamento, uma vez que a associação do híbrida do Azure AD é um elemento-chave que suporta a cogestão, os administradores do Configuration Manager trabalharam com a equipe de identidades. Esta empresa de software tinha muitas regras do ADFS e algumas delas eram complexas. Para abordar este desafio, a equipe de identidades revisto as regras existentes do AD FS antes de ativar a associação do Azure AD híbrido. A equipe de TI também optar por atualizar o Azure AD Connect para a versão mais recente. Agora, o Azure AD Connect fornece um fluxo de processo automatizado para ativar a associação ao Azure AD híbrido.

Após a implementação com êxito e o teste no respetivo ambiente de pré-produção, esse cliente ativado a associação do Azure AD híbrido para o estado de produção completo. Uma semana, tinham de todos os dispositivos Windows 10 geridos conjuntamente.



## <a name="contact-fasttrack"></a>Entre em contato com FastTrack

Se precisar de configuração de assistência do Azure AD em qualquer ponto do processo, aceda a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sessão e pedir assistência. 

Para obter mais informações, consulte [Obtenha ajuda de FastTrack](/sccm/comanage/quickstart-fasttrack). 

