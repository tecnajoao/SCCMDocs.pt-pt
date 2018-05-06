---
title: Privacidade e segurança do perfil de certificado
titleSuffix: Configuration Manager
description: Saiba mais sobre a segurança melhores práticas para gerir perfis de certificados para utilizadores e dispositivos no System Center Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d5e9d10844a344ea56eaebb315c92675a760c983
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-certificate-profiles-in-system-center-configuration-manager"></a>Segurança e privacidade para perfis de certificado no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Procedimentos Recomendados de Segurança para Perfis de Certificado  
 Utilize os seguintes procedimentos recomendados de segurança ao gerir perfis de certificado para utilizadores e dispositivos.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Identifique e siga os eventuais procedimentos recomendados de segurança do Serviço de Inscrição de Dispositivos de Rede, que incluem a configuração do Web site do Serviço de Inscrição de Dispositivos de Rede nos Serviços de Informação Internet (IIS) para que exija SSL e ignore os certificados de cliente.|Consulte [Orientação do Serviço de Inscrição de Dispositivos de Rede](http://go.microsoft.com/fwlink/p/?LinkId=309016) na biblioteca Serviços de Certificados do Active Directory na TechNet.|  
|Ao configurar os perfis de certificado SCEP, escolha as opções mais seguras suportadas pelos dispositivos e pela infraestrutura.|Identifique, implemente e siga os procedimentos de segurança eventualmente recomendados para os dispositivos e para a infraestrutura.|  
|Especifique manualmente a afinidade dispositivo/utilizador em vez de permitir que os utilizadores identifiquem o respetivo dispositivo primário. Além disso, não ative a configuração baseada na utilização.|Se clicar na opção **Permitir inscrição de certificados apenas no dispositivo primário dos utilizadores** num perfil de certificado SCEP, não considere autoritativas as informações recolhidas junto dos utilizadores ou do dispositivo. Se implementar perfis de certificado SCEP com esta configuração e um utilizador administrativo fidedigno não especificar a afinidade dispositivo/utilizador, os utilizadores não autorizados poderão obter privilégios elevados e certificados para autenticação.<br /><br /> **Nota:** Se ativar a configuração baseada na utilização, estas informações serão obtidas utilizando mensagens de estado que não são protegidas pelo System Center Configuration Manager. Para ajudar a atenuar esta ameaça, utilize a assinatura SMB ou IPsec entre computadores cliente e o ponto de gestão.|  
|Não adicione permissões de Leitura e Inscrição para utilizadores aos modelos de certificado ou configure o ponto de registo de certificados para ignorar a verificação do modelo de certificado.|Apesar do Configuration Manager suporta a verificação adicional se adicionar as permissões de segurança de leitura e inscrição para utilizadores e pode configurar o ponto de registo de certificados para ignorar esta verificação se a autenticação não for possível, nenhuma destas configurações constitui uma melhor prática de segurança. Para mais informações, veja [Planear permissões de modelo de certificado para perfis de certificado no System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Informações de Privacidade para Perfis de Certificado  
 Poderá utilizar perfis de certificado para implementar certificados de autoridade de certificação (AC) de raiz e de cliente, avaliando em seguida se esses dispositivos ficam em conformidade após a aplicação dos perfis. O ponto de gestão envia as informações de compatibilidade para o servidor de site e o System Center Configuration Manager armazena essas informações na base de dados do site. As informações de conformidade incluem propriedades de certificado, tais como o nome do requerente e o thumbprint. As informações são encriptadas quando os dispositivos as enviam para o ponto de gestão, mas não são armazenadas em formato encriptado na base de dados do site. A base de dados mantém as informações até que a tarefa de manutenção do site **Eliminar Dados de Gestão de Configuração Desatualizados** as elimine, após o intervalo predefinido de 90 dias. Pode configurar o intervalo de eliminação. As informações de conformidade não são enviadas à Microsoft.  

 Perfis de certificado utilizam as informações que o Configuration Manager recolhe através da deteção. Para mais informações sobre as informações de privacidade para deteção, veja a secção **Informações de Privacidade para Deteção** em [Segurança e privacidade para o System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Os certificados emitidos para utilizadores ou dispositivos poderão permitir o acesso a informações confidenciais.  

 Por predefinição, os dispositivos não avaliam os perfis de certificado. Além disso, terá de configurar os perfis de certificado e implementá-los para os utilizadores ou dispositivos.  

 Antes de configurar os perfis de certificado, considere os requisitos de privacidade.  
