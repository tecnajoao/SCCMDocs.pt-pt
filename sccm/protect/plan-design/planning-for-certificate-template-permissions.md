---
title: "Planear permissões do modelo de certificado | Documentos do Microsoft"
description: "Saiba mais sobre o planeamento de permissões que é necessário configurar os modelos de certificado que utiliza o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
caps.latest.revision: 5
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 832be8c9fda727804f57e83768cd8799db722c67
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-system-center-configuration-manager"></a>Planeamento de permissões de modelo de certificado para perfis de certificado no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


As seguintes informações podem ajudar a planear a forma configurar permissões para os modelos de certificado que o System Center Configuration Manager utiliza quando implementar perfis de certificado.  

## <a name="default-security-permissions-and-considerations"></a>Considerações e permissões de segurança predefinidas  
 As permissões de segurança predefinidas que são necessárias para os modelos de certificado que o System Center Configuration Manager utilizará para solicitar certificados para utilizadores e dispositivos são os seguintes:  

-   Leitura e Inscrição para a conta usada pelo conjunto aplicacional do Serviço de Inscrição de Dispositivos de Rede  

-   Ler para a conta que executa a consola do System Center Configuration Manager  

 Para mais informações sobre estas permissões de segurança, consulte o artigo [infraestrutura de certificados de configurar](../deploy-use/certificate-infrastructure.md).  

 Quando utiliza esta configuração predefinida, os utilizadores e os dispositivos não podem solicitar diretamente certificados dos modelos de certificados e todos os pedidos devem ser iniciados pelo Serviço de Inscrição de Dispositivos de Rede. Esta é uma restrição importante, pois estes modelos de certificados devem ser configurados com a opção **Fornecer no pedido** no Requerente do certificado, o que significa que existe um risco de representação se um utilizador não autorizado ou um dispositivo comprometido solicitar um certificado. Na configuração predefinida, o Serviço de Inscrição de Dispositivos de Rede tem de iniciar este pedido. No entanto, este risco de representação permanece se o serviço que executa o Serviço de Inscrição de Dispositivos de Rede estiver comprometido. Para ajudar a evitar este risco, siga todos os procedimentos recomendados de segurança relativos ao Serviço de Inscrição de Dispositivos de Rede e ao computador que executa este serviço de função.  

 Se as permissões de segurança predefinidas não cumprirem os seus requisitos empresariais, tem outra opção para configurar as permissões de segurança nos modelos de certificados: Pode adicionar a leitura e inscrição permissões para utilizadores e computadores.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Adicionar permissões de Leitura e Inscrição para utilizadores e computadores  
 Adição de leitura e permissões de inscrição para utilizadores e computadores podem ser apropriadas se uma equipa separada gere a sua equipa de infraestrutura de (AC) de autoridade de certificação e que separe equipa pretender que a System Center Configuration Manager para verificar que os utilizadores têm uma conta de serviços de domínio do Active Directory válida antes de lhes enviar um perfil de certificado para pedir um certificado de utilizador. Para esta configuração, tem de especificar um ou mais grupos de segurança que contenham os utilizadores e conceder a estes grupos permissões de Leitura e Inscrição nos modelos de certificados. Neste cenário, o administrador da AC gere o controlo de segurança.  

 Do mesmo modo, é possível especificar um ou mais grupos de segurança que contenham contas de computador e conceder a estes grupos permissões de Leitura e Inscrição nos modelos de certificados. Se implementar um perfil de certificado de computador num computador que seja membro de domínio, a conta desse computador terá de receber permissões de Leitura e Inscrição. Estas permissões não são necessárias se o computador não é um € de memberâ domínio "por exemplo, se for um computador de grupo de trabalho ou um dispositivo móvel pessoal.  

 Embora esta configuração utilize um controlo de segurança adicional, não a aconselhamos como procedimento recomendado. O motivo é que os utilizadores especificados ou os proprietários dos dispositivos podem solicitar certificados de forma independente a partir do System Center Configuration Manager e valores de alimentação para o requerente do certificado que pode ser utilizado para representar outro utilizador ou dispositivo.  

 Além disso, se especificar contas que não podem ser autenticadas no momento em que ocorre o pedido de certificado, o pedido de certificado falhará por predefinição. Por exemplo, o pedido de certificado falhará se o servidor que executar o Serviço de Inscrição de Dispositivos de Rede estiver numa floresta do Active Directory que não é fidedigna para a floresta que contém o servidor do sistema de sites do ponto de registro de certificados. Pode configurar o ponto de registo de certificados para continuar se não for possível autenticar uma conta por não existir resposta do controlador de domínio. No entanto, este não é um procedimento recomendado de segurança.  

 De notar que, se o ponto de registo de certificados estiver configurado para verificar permissões de conta e se um controlador de domínio estiver disponível e rejeitar o pedido de autenticação (por exemplo, a conta está bloqueada ou foi eliminada), o pedido de inscrição de certificados falhará.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Para verificar permissões de Leitura e Inscrição para utilizadores e computadores membros de domínio  

1.  No servidor de sistema de sites que aloja o ponto de registo de certificados, crie a seguinte chave de registo DWORD para ter um valor de 0: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Se não for possível autenticar uma conta por não existir resposta do controlador de domínio e pretender ignorar a verificação das permissões:  

    -   No servidor de sistema de sites que aloja o ponto de registo de certificados, crie a seguinte chave de registo DWORD para ter um valor de 1: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  Na AC emissora, no separador **Segurança** das propriedades do modelo de certificado, adicione um ou mais grupos de segurança para conceder permissões de Leitura e Inscrição às contas de utilizador ou de dispositivo.  
