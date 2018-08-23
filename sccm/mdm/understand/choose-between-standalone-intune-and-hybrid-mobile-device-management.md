---
title: Escolha o Intune autónomo ou MDM híbrida
titleSuffix: Configuration Manager
description: Escolha se pretende implementar a gestão de dispositivos móveis híbrida com o Intune e Configuration Manager ou executar o Intune autónomo.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 153c1208cef8a940cc06412322e8112d53d17e58
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/14/2018
ms.locfileid: "42586282"
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mdm-with-configuration-manager"></a>Escolher entre o Microsoft Intune autónomo e a MDM híbrida com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma das mais freqüentes perguntas sobre a gestão de dispositivos móveis (MDM) com o Microsoft Intune é "Deve posso integrar o Intune com o Configuration Manager (MDM híbrida) ou executar o Intune autónomo na configuração de apenas de nuvem?" 

O Intune no Azure é a solução MDM recomendada da Microsoft.     


> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


 
## <a name="intune-standalone"></a>Intune autónomo

Intune autónomo é a topologia de implementação recomendada da Microsoft. Intune autónomo é uma solução MDM apenas na cloud que gere com uma consola web acedida em qualquer parte do mundo. Centros de dados do Intune estão alojados na América do Norte, Europa e Ásia. Como o Intune é um serviço em nuvem, pode implementar rapidamente a gestão do Intune para os seus dispositivos.

Os clientes geralmente encontrá-lo mais rápido e fácil de implementar a topologia de autónoma porque não existe nenhuma dependência de componentes no local. Intune autónomo é agora na plataforma de cloud do Microsoft Azure e fornece muitos recursos avançados, tais como:  

- Plataforma de gestão de mobilidade empresarial integrado: Uma plataforma de cloud integrados e administrador de experiência no portal do Azure para o Intune, o Azure AD Premium e o Azure Information Protection  

- Gestão de dispositivos móveis: Capacidades de proteção de informações e gestão avançada de dispositivos móveis  

- Dimensionamento: Implementar e gerir dispositivos móveis sem se preocupar em escala  

- Controlo de acesso baseado em funções: Restringir o acesso a funções administrativas com base em funções atribuídas e âmbitos  

- Acesso programático (API): Suporte do Microsoft Graph API e as opções de gestão do SDK e o PowerShell  

- Consola Web: Uma consola baseada em HTML 5 normas da web com suporte para a maioria dos browsers modernos  

- Relatórios avançados: Capacidade de criar relatórios personalizados  

- Agilidade: Configuração simples e entrega rápida de novos recursos  



## <a name="hybrid-mdm-with-configuration-manager"></a>MDM híbrida com o Configuration Manager

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).  

MDM híbrido é uma solução que se integra capacidades de gestão de dispositivos móveis do Intune para o Configuration Manager. Ele utiliza o Intune como o canal de entrega de políticas, perfis e aplicações em dispositivos, mas utiliza a infraestrutura do Configuration Manager no local para administrar o conteúdo e gerir os dispositivos. Numa implementação híbrida proporciona controle "único painel de vidro". Isso significa que pode utilizar a mesma infraestrutura no local e o console de administração para gerir dispositivos móveis com o Intune, bem como PCs e servidores com o cliente do Configuration Manager tradicional. 

Pode escolher a MDM híbrida pelos seguintes motivos:  

- Quiser gerir ambos os dispositivos móveis inscritos no Intune e dispositivos geridos com o cliente do Configuration Manager no mesmo console administrativo  

- Sua infraestrutura exige que tenha de múltiplos servidores do NDES para disponibilização de certificado em dispositivos móveis  

- Sua infraestrutura exige que tenha vários conectores do Exchange  

- Exigir o suporte de encriptação S/MIME

> [!Note]  
> Se configurar a MDM híbrida no Configuration Manager para o acesso condicional com o Exchange no local, os utilizadores ainda podem aceder a e-mail no Outlook para iOS e Android. Esta configuração mesmo com o e-mail de blocos do Intune autónomo para estes clientes.<!--Intune bug 2285890-->  



## <a name="change-the-mdm-authority"></a>Alterar a autoridade MDM

Se precisar de alterar a definição de autoridade MDM, pode alterá-lo mesmo sem ter de contactar Support da Microsoft e sem ter de anular a inscrição e inscrever novamente os seus dispositivos geridos existentes. Para obter detalhes, consulte [alterar a sua autoridade MDM](/sccm/mdm/deploy-use/change-mdm-authority).

