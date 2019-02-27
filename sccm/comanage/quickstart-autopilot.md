---
title: Windows Autopilot com cogestão
titleSuffix: Configuration Manager
description: Utilize o Windows Autopilot com cogestão no Configuration Manager para simplificar o conjunto de cópia de segurança de novos dispositivos Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28710b925444d681a161eff184b845a1cdd430b1
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838757"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot com cogestão

Receber um novo dispositivo Windows 10 é empolgante. No entanto, pode demorar tempo para configurar as definições e aplicações para que possa ser produtivo. Cogestão resolve este problema com o Windows Autopilot de aprovisionamento de dispositivos.

Autopilot fornece uma experiência simplificada para e seus usuários nas seguintes situações:
- Configurar e pré-configurar novos dispositivos Windows 10  
- Repor, reciclagem e recuperar dispositivos existentes  

Autopilot reduz o tempo, recursos e complexidade associada à implantação, gerenciamento e a extinção de dispositivos. Ao mesmo tempo, a experiência para seus usuários é simplificado e fácil de primeiro arranque.

Windows Autopilot oferece suporte a vários cenários, todos os quais estão maximizados com cogestão:

- Os utilizadores podem orientar suas próprias Implantações de novos dispositivos em qualquer um dos Active Directory com a associação do híbrida do Azure AD ou Azure Active Directory (Azure AD)  

- Pode configurar o Self-implementar novas Implantações de dispositivos com o Azure AD para dispositivos partilhados e quiosques  

- Com o Windows Autopilot para dispositivos existentes, utilizar o Gestor de configuração para migrar um dispositivo existente do Windows 7 e o Active Directory para Windows 10 e o Azure AD  

No vídeo seguinte, Danny Guillory do gerente de programas sênior e gerente de programa principal Andrew McMurray discutem e demonstrar Windows Autopilot com cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Quando utiliza a cogestão e Autopilot em conjunto, certifique-se de que novos dispositivos introduzir a sua rede acabam no mesmo Estado de gestão. Nessa configuração, os dispositivos estão inscritos no Intune e que um cliente do Configuration Manager.  Permite-lhe utilizar o novo modelo de aprovisionamento do Windows 10 e ajuda-o a eliminar a necessidade de criar, manter e atualizar imagens do sistema operacional personalizadas. 

Em todos estes cenários, pode automaticamente [ativar a cogestão](/sccm/comanage/how-to-prepare-win10) pelo Intune. Essa automatização ajuda com o processo de aprovisionamento e para o gerenciamento contínuo do dispositivo.

Com Autopilot, não precisa se preocupar sobre controladores e imagens. Concentre-se o aprovisionamento de dispositivos por esse processo automatizado com o Intune e Configuration Manager através de cogestão.


Eis como uso cogestão e o Autopilot em conjunto pode ajudá-lo neste momento:

#### <a name="reduce-time-costs-and-complexity"></a>Reduzir o tempo, os custos e complexidade
Windows Autopilot utiliza a versão com otimização de OEM do Windows 10, que é pré-instalado no dispositivo. Esta configuração salva as organizações, o esforço de ter de manter imagens personalizadas e controladores para cada modelo de dispositivo em utilização. Em vez de recriar a imagem do dispositivo, transforme a instalação do Windows 10 existente para um Estado "pronto". Aplica-se as definições e políticas, instala aplicações e altera a edição do Windows 10. Por exemplo, atualização do Windows 10 Pro para Windows 10 Enterprise, para que pode dar suporte a funcionalidades avançadas.

#### <a name="improve-the-user-experience"></a>Melhorar a experiência de utilizador
A melhor experiência de usuário faz com que a interrupção, pelo menos e ajuda a obter de volta nos concentrar em seu trabalho. Windows Autopilot oferece uma abordagem simple para ajudar os seus utilizadores configurar rapidamente com apenas alguns cliques e as credenciais do Azure AD. Para muitas organizações com um campo grande de funcionários remotos, use o Windows Autopilot para lançar novos dispositivos diretamente a partir do fabricante.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Utilizar o Autopilot e o Configuration Manager para migrar dispositivos existentes do Windows 7 para Windows 10
Com o Windows Autopilot para dispositivos existentes, criar um ficheiro de configuração e implementá-la com uma sequência de tarefas do Configuration Manager. Este processo migra facilmente dispositivos existentes do Windows 7 para Windows 10. Utilizar uma imagem de assinatura com o Windows 10 no Configuration Manager e, em seguida, aplicá-la para os dispositivos existentes do Windows 7 com a configuração do Autopilot. Quando o usuário inicia o dispositivo, eles usam o processo de integração de controlada pelo usuário do Autopilot.

Eis os passos para Autopilot para dispositivos existentes:

![Visão geral do processo para o Windows Autopilot para dispositivos existentes](media/autopilot-for-existing-devices.png)

1. Implementar a política de grupo para redirecionamento de pastas conhecidas para o OneDrive
2. Gerar ficheiro de configuração do Autopilot
3. Implementar a sequência de tarefas para atualizar para o Windows 10
4. Máquina do Windows 10 atravessa o Autopilot no primeiro arranque

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernizando o aprovisionamento de dispositivos para todos os tipos de funções de trabalho
Com o Autopilot, agora pode fornecer uma implementação de sistema operacional automatizada para dispositivos unmanned ou dispositivos partilhados com o modo de implementação automática. Esta configuração cumpre as necessidades de todos os seus tipos diferentes de funções de trabalho. Além disso, a função de reposição do Windows Autopilot certifica-se de que o reprovisionamento de um dispositivo para um novo utilizador é simples e fácil. Este processo simplifica o que tem sido tradicionalmenta uma tarefa difícil quando tem sazonais ou funções de trabalho de contrato. 



## <a name="case-study"></a>Estudo de caso

A empresa de prestadores de logística e rail alemão DB Shenker utiliza o Autopilot para aumentar a produtividade dos funcionários e liberar sua as equipas de TI por trabalhar em tarefas diárias de suporte. Shenker foi movido para fora de geração de imagens tradicional e o substitui pelo aprovisionamento por meio da nuvem. Agora que utilizar o Azure AD join e o Intune para obter a trabalhar rapidamente a novos dispositivos. 

Em vez de ter o seu tempo de desperdício de funcionários remotos em trânsito para uma localização com serviços de TI, Shenker utiliza agora o Windows Autopilot. Eles envie seu hardware de funções de trabalho diretamente a partir do fabricante para seus escritórios de campo local. A função de trabalho do novo dispositivo estabelece ligação à internet e que iniciar sessão com as credenciais do Azure AD. O dispositivo, em seguida, liga-se para as aplicações e serviços que Schenker atribui do departamento de TI para o perfil de utilizador individuais.

Para obter mais informações, consulte [centraliza a empresa de logística Global IT, une os funcionários com área de trabalho digital moderna](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Proposta de valor

Crie satisfação na sua organização através da criação de uma melhor experiência de utilizador para os seus utilizadores. Utilize o Windows Autopilot para reduzir os custos. Libere sua equipe se concentrar em outros projetos extraiam mais valor e impacto para a sua organização.



## <a name="configure"></a>Configurar

Para obter mais informações, veja os artigos seguintes:

[Utilizar o Intune para criar perfis do Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

[Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices) sequência de tarefas

