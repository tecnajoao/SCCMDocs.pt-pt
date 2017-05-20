---
title: "Extensões de esquema | Documentos do Microsoft"
description: Expanda o esquema do Active Directory para suportar o System Center Configuration Manager.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
ms.translationtype: Machine Translation
ms.sourcegitcommit: 7479e54b5db2eff893bf9fbaf52c104836cda519
ms.openlocfilehash: 5b5540c35c02df6e3d06e4aa9269b8da3238233e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>Extensões de esquema para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode expandir o esquema do Active Directory para suportar o Configuration Manager. Isto edita o esquema do Active Directory de uma floresta para adicionar um novo contentor e muitos outros atributos que utilizar sites do Configuration Manager para publicar as informações de chaves no Active Directory onde os clientes podem utilizar segura-lo. Esta informação pode simplificar a implementação e configuração de clientes os clientes e ajuda-o a localizar recursos do site, como servidores com o conteúdo implementado ou que fornecem diferentes serviços aos clientes.  

-   É uma boa ideia expandir o esquema do Active Directory, mas não é necessário.  

Antes de [expandir o esquema do Active Directory](https://msdnstage.redmond.corp.microsoft.com/en-US/library/mt345589\(TechNet.10\).aspx), deve estar familiarizado com os Serviços de Domínio do Active Directory e à vontade para [modificar o esquema do Active Directory](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Considerações para expandir o esquema do Active Directory para o Configuration Manager  

-   As extensões de esquema do Active Directory para o System Center Configuration Manager são iguais às que utilizam o Configuration Manager 2007 e do Configuration Manager 2012. Caso tenha expandido anteriormente o esquema de uma das versões, não precisa de expandir novamente o esquema.  

-   Expandir o esquema é uma ação de toda a floresta, única e irreversível.  

-   Apenas um utilizador que seja um membro do grupo Admins de esquemas ou a quem tenham sido delegadas permissões suficientes para alterar o esquema pode expandir o esquema.  

-   Embora pode expandir o esquema antes ou depois de executar a configuração do Configuration Manager, é uma boa ideia expandir o esquema antes de começar a configurar os seus sites e definições de hierarquia. Isto poderá simplificar muitos passos de configuração posteriores.  

-   Depois de expandir o esquema, o catálogo global do Active Directory é replicado em toda a floresta. Por conseguinte, planeie expandir o esquema quando o tráfego de replicação não afetarão negativamente outros processos dependentes da rede:  

    -   Em florestas do Windows 2000, a expansão do esquema provoca uma sincronização completa de todo o catálogo global.  

    -   A partir das florestas do Windows 2003, são replicados apenas os atributos adicionados recentemente.  

**Dispositivos e clientes que não utilizam o esquema do Active Directory:**  

-   Dispositivos móveis geridos pelo conector do Exchange Server  

-   O cliente para computadores Mac  

-   O cliente para servidores Linux e UNIX  

-   Dispositivos móveis que são inscritos pelo Configuration Manager  

-   Dispositivos móveis que são inscritos pelo Microsoft Intune  

-   Clientes legados do dispositivo móvel  

-   Clientes do Windows que estão configurados para gestão de clientes apenas de Internet  

-   Clientes Windows detetados pelo Configuration Manager na Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Capacidades que beneficiam da expansão do esquema  
**Cliente computador instalação e atribuição de site** -computador Windows de quando instala um novo cliente, o cliente procura serviços de domínio do Active Directory para as propriedades de instalação.  

-   **Soluções:** Se não expandir o esquema, utilize uma das seguintes opções para fornecer detalhes de configuração que computadores têm de instalar:  

    -   **Utilize a instalação push de cliente**. Antes de utilizar um método de instalação de cliente, certifique-se de que todos os pré-requisitos são cumpridos. Para mais informações, consulte a secção 'Dependências do método de instalação' [pré-requisitos para implementação de clientes para computadores com o Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers).  

    -   **Instalar manualmente clientes** e forneça as propriedades de instalação do cliente utilizando as propriedades da linha de comandos de instalação de CCMSetup. Isto deve incluir o seguinte:  

        -   Especifique um caminho de origem ou de ponto de gestão a partir do qual o computador pode transferir os ficheiros de instalação utilizando a propriedade de CCMSetup **/mp: =&lt;nome do nome de computador do ponto de gestão\>**  ou **/Source:&lt;caminho para ficheiros de origem do cliente\> ** na linha de comandos do CCMSetup durante a instalação do cliente.  

        -   Especifique uma lista dos pontos de gestão inicial para o cliente possa utilizar para que possa atribuir-lhes para o site e, em seguida, transferir as definições de política e o site do cliente. Para o efeito, utilize a propriedade SMSMP do CCMSetup Client.msi.  

    -   **Publique o ponto de gestão no DNS ou WINS** e configure clientes para utilizar este método de localização do serviço.  

**Configuração da porta para comunicação cliente-servidor** - quando instala um cliente, este é configurado com informações da porta armazenadas no Active Directory. Se posteriormente alterar a porta de comunicação cliente-servidor de um site, um cliente pode obter esta nova definição da porta dos serviços de domínio do Active Directory.  

-   **Soluções:** Se não expandir o esquema, utilize uma das seguintes opções para fornecer as novas configurações porta aos clientes existentes:  

    -   **Reinstale os clientes** utilizando opções de configurar a porta nova.  

    -   **Implemente um script personalizado nos clientes para atualizar as informações da porta**. Se os clientes não conseguirem comunicar com um site devido a uma alteração da porta, é possível utilizar o Configuration Manager para implementar este script. Por exemplo, pode utilizar a Política de Grupo.  

**Cenários de implementação de conteúdo** - quando cria conteúdo num site e, em seguida, implementar que conteúdo para outro site na hierarquia, o site recetor deve ter capacidade para verificar a assinatura dos dados do conteúdo assinados. Isto requer acesso à chave pública do site de origem onde são criados estes dados. Quando expande o esquema do Active Directory para o Configuration Manager, a chave pública do site está disponível para todos os sites na hierarquia.  

-   **Solução:** Se não expandir o esquema, utilize a ferramenta manutenção da hierarquia, **preinst.exe**, para trocar as informações da chave seguras entre sites.  

     Por exemplo, se pretender criar conteúdo num site primário e implementar este conteúdo a um site secundário abaixo de um site primário diferente, terá de expandir num esquema do Active Directory para permitir que o site secundário, obtém a origem principal chave pública do site ou utilize preinst.exe para partilhar as chaves diretamente entre os dois sites.  

## <a name="active-directory-attributes-and-classes"></a>Classes e atributos do Active Directory  
Quando expande o esquema para o System Center Configuration Manager, os atributos e classes seguintes são adicionados para o esquema e estão disponíveis para todos os sites do Configuration Manager nessa floresta do Active Directory.  

-   Atributos:  

    -   CN = mS-SMS-atribuição--código do Site  

    -   CN = capacidades de SMS mS  

    -   CN = MS--predefinição-MP do SMS  

    -   CN = mS-SMS---ponto de gestão dispositivos  

    -   CN = mS--estado de funcionamento-estado do SMS  

    -   CN = MS-SMS-MP-endereço  

    -   CN = MS-SMS--nome do MP  

    -   CN = MS-SMS-Ranged-IP-alta  

    -   CN = MS-SMS-Ranged-IP-baixa  

    -   CN = MS-SMS-Roaming-limites  
        em  

    -   CN = MS-SMS--limites do Site  

    -   CN = MS-SMS--código do Site  

    -   CN = mS SMS-origem florestas  

    -   CN = SMS-mS-Version  

-   Classes:  

    -   CN = MS---ponto de gestão SMS  

    -   CN = MS-SMS-Roaming-limites-intervalo  

    -   CN = MS-SMS--ponto localizador de servidor  

    -   CN = MS-Site de SMS  

> [!NOTE]  

>  As extensões de esquema podem incluir atributos e classes provenientes de versões anteriores do produto, mas não utilizados pelo System Center Configuration Manager. Por exemplo:  

>   
>  -   Atributo: cn = MS-SMS--limites do Site  
> -   Classe: cn = MS-SMS--ponto localizador de servidor  

Pode garantir as anteriores listas estão atualizadas visualizando a **ConfigMgr_ad_schema. LDF** ficheiro a partir do **\smssetup\bin\x64.** pasta do suporte de instalação do System Center Configuration Manager.  

