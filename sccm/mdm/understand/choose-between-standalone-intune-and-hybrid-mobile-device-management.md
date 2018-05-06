---
title: Escolha o Intune autónomo ou o MDM híbrido
titleSuffix: Configuration Manager
description: Escolha se pretende implementar a gestão de dispositivos móveis híbrida com o Intune e Configuration Manager ou executar o Intune autónomo.
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a7cd26fde23c560295117edcc148835b1397a55
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Escolher entre o Microsoft Intune de autónomo e híbrida de gestão de dispositivos móveis com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma das mais frequentemente mais frequentes perguntas sobre a gestão de dispositivos móveis (MDM) com o Microsoft Intune é "Deve posso integrar o Intune com o Configuration Manager (MDM híbrido) ou execute o Intune autónomo na configuração apenas na nuvem?" Para responder a essa questão, deve comparar cuidadosamente as duas opções.
 
## <a name="intune-standalone"></a>Intune autónomo
Intune autónomo é a topologia de implementação recomendada da Microsoft. Intune autónomo é uma solução MDM apenas de nuvem e for gerido em qualquer lugar a utilizar uma consola web que pode ser acedida a partir do mundo. Intune centros de dados estão alojados na América do Norte, Europa e Ásia. Porque o Intune é um serviço em nuvem, pode implementar a gestão do Intune nos seus dispositivos num período de tempo relativamente curto.

Os clientes geralmente encontrá-lo mais rápido e mais fácil de implementar a topologia de autónoma porque não há nenhum dependência de componentes no local. Intune autónomo é agora na plataforma de nuvem do Microsoft Azure e fornece várias funcionalidades avançadas, tais como:
- Experiência integrada enterprise mobility plataforma de gestão - uma plataforma em nuvem integrado e administração no portal do Azure para o Intune, Azure AD Premium e do Azure Information Protection.
- Gestão de dispositivos móveis - capacidades de proteção de informações e gestão de dispositivos móveis avançada.
- Dimensionar - implementar e gerir dispositivos móveis sem se preocupar escala.
- Controlo de acesso baseado em funções – restringir o acesso com base nas funções atribuídas e âmbitos de funções administrativas.
- Acesso programático (API) - suporte de Microsoft Graph API e as opções de gestão do SDK e PowerShell.
- Consola Web - com base no HTML 5 de uma consola incorporada no normas web com suporte para mais modernos browsers da web.
- Avançadas reporting - capacidade de criar relatórios personalizados.
- Agilidade - configuração simples e rápida entrega novas capacidades.


## <a name="hybrid-mdm-with-configuration-manager"></a>MDM com o Gestor de configuração híbrido
MDM híbrido é uma solução que se integra capacidades de gestão de dispositivos móveis do Intune para o Configuration Manager. Se utiliza o Intune como o canal de entrega de políticas, perfis e aplicações em dispositivos, mas utiliza a infraestrutura no local do Configuration Manager para administrar o conteúdo e gerir os dispositivos. Uma implementação híbrida dá-lhe controlo "painel único de transparência".  Isto significa que pode utilizar a mesma infraestrutura no local e a consola administrativa para gerir dispositivos móveis com o Intune, bem como PCs e servidores com o cliente do Configuration Manager tradicional. Pode optar por MDM híbrido pelos seguintes motivos:  
- Quiser gerir dispositivos móveis inscritos no Intune e dispositivos geridos com o cliente do Configuration Manager a partir da consola administrativa do mesmo
- A infraestrutura requer que tem vários servidores NDES para entrega de certificados para dispositivos móveis
- Requer que a infraestrutura que tem vários conectores do Exchange
- Necessitar de suporte de encriptação S/MIME


## <a name="changing-the-mdm-authority-setting"></a>Alterar a definição de autoridade MDM
Se precisar de alterar a definição de autoridade MDM, pode alterá-lo por si sem ser necessário contactar Support da Microsoft e sem ter de anular a inscrição e inscrever-se novamente os seus dispositivos geridos existentes. Para obter mais informações, consulte [alterar a autoridade de MDM](../deploy-use/change-mdm-authority.md).

> [!NOTE]    
> Tem de ter o Configuration Manager versão 1610 ou posterior para alterar a autoridade de MDM ao Intune autónomo. Quando tiver uma versão anterior do Configuration Manager, pode alterar a autoridade de MDM, mas necessita de ajuda do suporte da Microsoft e de operações. Também requer anular a inscrição e inscrever-se novamente todos os seus dispositivos após a autoridade de MDM é alterada.  
