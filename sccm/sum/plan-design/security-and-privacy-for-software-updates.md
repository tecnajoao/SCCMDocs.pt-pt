---

title: "Segurança e privacidade para atualizações de software | Documentos do Microsoft"
description: "Siga estas melhores práticas de segurança para atualizações de software e saiba mais sobre como do Configuration Manager processa as informações de privacidade."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
ms.translationtype: Machine Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 4b4f045138abc14b6e93b3b990c5f3a8b4f2f952
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017



---
# <a name="security-and-privacy-for-software-updates-in-system-center-configuration-manager"></a>Segurança e privacidade para atualizações de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações de privacidade para atualizações de software no System Center Configuration Manager e segurança.  

##  <a name="BKMK_Security_HardwareInventory"></a> Procedimentos recomendados de segurança para atualizações de software  
 Utilize os seguintes procedimentos recomendados de segurança para implementar atualizações de software em clientes:  

-   Não altere as permissões predefinidas nos pacotes de atualização de software.  

     Por predefinição, os pacotes de atualização de software são configurados para permitir **Controlo Total** aos administradores e acesso de **Leitura** aos utilizadores. Se alterar estas permissões, poderá permitir que um intruso adicione, remova ou elimine as atualizações de software.  

-   Controle o acesso à localização de transferência de atualizações de software.  

     As contas de computador do Fornecedor de SMS, o servidor do site e o utilizador administrativo que efetivamente transferem atualizações de software para a localização de transferência necessitam de acesso de **Escrita** a essa mesma localização. Restrinja o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem das atualizações de software por parte de intrusos.  

     Além disso, se utilizar uma partilha UNC na localização de transferência, proteja o canal de rede utilizando o IPsec ou a assinatura SMB para evitar a adulteração dos ficheiros de origem de atualizações de software quando forem transferidos através da rede.  

-   Utilize a UTC para avaliar a tempos de implementação.  

     Se utilizar a hora local em vez da UTC, os utilizadores poderão atrasar a instalação das atualizações de software alterando o fuso horário nos respetivos computadores  

-   Ative SSL no WSUS e siga os procedimentos recomendados para proteger o Windows Server Update Services (WSUS).  

     Identifique e siga os procedimentos de segurança para a versão do WSUS que utiliza com o Configuration Manager.  

    > [!IMPORTANT]  
    >  Se configurar o ponto de atualização de software para ativar as comunicações SSL no servidor WSUS, tem de configurar as raízes virtuais para SSL no servidor WSUS.  

-   Ative a verificação CRL.  

     Por predefinição, o Configuration Manager não verifica a lista de revogação de certificados (CRL) para confirmar a assinatura nas atualizações de software antes da respetiva implementação nos computadores. A verificação da CRL sempre que é utilizado um certificado oferece mais segurança contra a utilização de um certificado revogado, mas provoca um atraso de ligação e implica um processamento adicional no computador que a está a efetuar.  

     Para obter mais informações sobre como ativar a CRL procurar atualizações de software, consulte o artigo [como ativar a verificação CRL para atualizações de software no System Center Configuration Manager](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Configure o WSUS para utilizar um Web site personalizado.  

     Quando instala o WSUS no ponto de atualização de software, pode optar por utilizar o Web site predefinido do IIS existente ou por criar um Web site do WSUS personalizado. Crie um Web site personalizado para o WSUS para que o IIS aloje os serviços WSUS num Web site virtual dedicado em vez de partilhar o mesmo web site que é utilizada pelos outros sistemas de sites do Configuration Manager ou outras aplicações.  

     Para obter mais informações, consulte o artigo [configurar o WSUS para utilizar um web site personalizado](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="BKMK_Privacy_HardwareInventory"></a>Informações de privacidade para atualizações de software  
 As atualizações de software analisam os computadores cliente para determinar que atualizações de software são necessárias e, em seguida, devolvem as informações à base de dados do site. Durante o processo de atualizações de software do Configuration Manager pode transmitir informações entre clientes e servidores que identificam as contas de computador e de início de sessão.  

 O Configuration Manager mantém as informações de estado sobre o processo de implementação de software. As informações de estado não são encriptadas durante a transmissão ou o armazenamento. As informações de estado são armazenadas na base de dados do Configuration Manager e serem eliminadas pelas tarefas de manutenção da base de dados. Não são enviadas informações de estado à Microsoft.  

 A utilização de atualizações de software do Configuration Manager para instalar atualizações de software em computadores cliente pode estar sujeita aos termos de licenciamento do software dessas atualizações, que são separado dos termos de licenciamento de Software para o System Center Configuration Manager. Reveja e aceite os termos de licenciamento para Software antes de instalar as atualizações de software através do Configuration Manager sempre.  

 Configuration Manager não implementa atualizações de software por predefinição e requer vários passos de configuração antes de informações que são recolhidas.  

 Antes de configurar as atualizações de software, considere os requisitos de privacidade.  
