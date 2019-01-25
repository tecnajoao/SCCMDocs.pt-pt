---
title: Extensões de esquema
titleSuffix: Configuration Manager
description: Expanda o esquema do Active Directory para suportar o System Center Configuration Manager.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af7ddd4bd40fb60efa58fb78e20ee587aca9d4f5
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897649"
---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>Extensões de esquema para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode estender o esquema do Active Directory para suportar o Configuration Manager. Isto edita o esquema do Active Directory de uma floresta para adicionar um novo contentor e vários atributos que utilizam a sites do Configuration Manager para publicar informações chave no Active Directory em que os clientes podem em segurança a utilizam. Esta informação pode simplificar a implementação e configuração de clientes de clientes e ajuda a localizar recursos de site, como servidores com o conteúdo implementado ou que fornecem serviços diferentes aos clientes.  

-   É uma boa idéia para expandir o esquema do Active Directory, mas não seja necessário.  

Antes de [expandir o esquema do Active Directory](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema), deve estar familiarizado com os Serviços de Domínio do Active Directory e à vontade para [modificar o esquema do Active Directory](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Considerações para expandir o esquema do Active Directory para o Configuration Manager  

-   As extensões de esquema do Active Directory para o System Center Configuration Manager são iguais às que utilizam o Configuration Manager 2007 e o Configuration Manager 2012. Caso tenha expandido anteriormente o esquema de uma das versões, não precisa de expandir novamente o esquema.  

-   A extensão do esquema é uma ação de toda a floresta, única e irreversível.  

-   Apenas um utilizador que seja membro do grupo de Admins de esquemas ou a quem tenham sido delegadas permissões suficientes para alterar o esquema pode expandir o esquema.  

-   Embora seja possível estender o esquema antes ou depois de executar a configuração do Configuration Manager, é uma boa idéia para expandir o esquema antes de começar a configurar seus sites e definições de hierarquia. Isto poderá simplificar muitos passos de configuração posteriores.  

-   Depois de expandir o esquema, o catálogo global do Active Directory é replicado em toda a floresta. Por conseguinte, planeie expandir o esquema quando o tráfego de replicação não afete negativamente outros processos dependentes da rede:  

    -   Em florestas do Windows 2000, a expansão do esquema provoca uma sincronização completa de todo o catálogo global.  

    -   A partir das florestas do Windows 2003, são replicados apenas os atributos adicionados recentemente.  

**Dispositivos e clientes que não usam o esquema do Active Directory:**  

-   Dispositivos móveis geridos pelo conector do Exchange Server  

-   O cliente para computadores Mac  

-   O cliente para servidores Linux e UNIX  

-   Dispositivos móveis inscritos pelo Configuration Manager  

-   Dispositivos móveis inscritos pelo Microsoft Intune  

-   Clientes legados do dispositivo móvel  

-   Clientes do Windows que estão configurados para gestão de clientes apenas de Internet  

-   Clientes do Windows que são detetados pelo Configuration Manager para ser na Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Capacidades que beneficiam da expansão do esquema  
**Atribuição de site e de instalação de computador do cliente** -computador Windows de um quando instala um novo cliente, o cliente procura de serviços de domínio do Active Directory para as propriedades de instalação.  

-   **Soluções alternativas:** Se não expandir o esquema, utilize uma das seguintes opções para fornecer os detalhes de configuração que computadores têm de instalar:  

    -   **Utilize a instalação push de cliente**. Antes de utilizar um método de instalação do cliente, certifique-se de que todos os pré-requisitos são cumpridos. Para obter mais informações, consulte a secção "Dependências do método de instalação" em [pré-requisitos para implementar clientes em computadores Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers).  

    -   **Instale manualmente os clientes** e forneça as propriedades de instalação do cliente, utilizando as propriedades de linha de comandos de instalação do CCMSetup. Isto deve incluir o seguinte:  

        -   Especifique um caminho de ponto ou origem de gestão do qual o computador pode transferir os ficheiros de instalação utilizando a propriedade de CCMSetup **/mp: =&lt;nome do computador do ponto de gestão\>**  ou **/ origem:&lt;caminho para os ficheiros de origem do cliente\>**  na linha de comandos CCMSetup durante a instalação de cliente.  

        -   Especifique uma lista de pontos de gestão inicial para o cliente para utilizar, para que ele pode atribuí-los para o site e, em seguida, transferir as definições de política e o site do cliente. Para o efeito, utilize a propriedade SMSMP do CCMSetup Client.msi.  

    -   **Publique o ponto de gestão no DNS ou WINS** e configure clientes para utilizar este método de localização do serviço.  

**Configuração da porta para comunicação cliente-servidor** - quando instala um cliente, este é configurado com informações da porta armazenadas no Active Directory. Se posteriormente alterar a porta de comunicação cliente-servidor para um site, um cliente pode obter esta nova definição de porta dos serviços de domínio do Active Directory.  

-   **Soluções alternativas:** Se não expandir o esquema, utilize uma das seguintes opções para fornecer novas configurações de porta aos clientes existentes:  

    -   **Reinstale os clientes** utilizando as opções que configuram a porta nova.  

    -   **Implemente um script personalizado nos clientes para atualizar as informações da porta**. Se os clientes não conseguirem comunicar com um site devido a uma alteração de porta, não é possível utilizar o Configuration Manager para implementar este script. Por exemplo, pode utilizar a Política de Grupo.  

**Cenários de implementação de conteúdo** - quando cria conteúdo num site e, em seguida, implementar que conteúdo noutro site da hierarquia, o site recetor deve ter capacidade para verificar a assinatura dos dados de conteúdo assinado. Isto requer acesso à chave pública do site de origem onde são criados estes dados. Quando expande o esquema do Active Directory para o Configuration Manager, chave pública de um site está disponível para todos os sites na hierarquia.  

-   **Solução:** Se não expandir o esquema, utilize a ferramenta de manutenção da hierarquia **preinst.exe**, para trocar as informações da chave seguras entre sites.  

     Por exemplo, se pretender criar conteúdo num site primário e implementado depois este conteúdo para um site secundário abaixo de um site primário diferente, tem de alargar o esquema do Active Directory para permitir que o site secundário, obter a chave pública de origem do site primário ou utilize preinst.exe para partilhar as chaves entre os dois sites diretamente.  

## <a name="active-directory-attributes-and-classes"></a>Classes e atributos do Active Directory  
Quando expande o esquema para o System Center Configuration Manager, as seguintes classes e atributos são adicionados ao esquema e está disponível para todos os sites do Configuration Manager nessa floresta do Active Directory.  

-   Atributos:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   CN = MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   CN = MS-SMS-Ranged-IP-baixa  

    -   cn=MS-SMS-Roaming-Boundaries  
        em  

    -   CN = MS-SMS--limites do Site  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Classes:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   CN = MS-Site do SMS  

> [!NOTE]
> 
>  As extensões de esquema podem incluir atributos e classes provenientes de versões anteriores do produto, mas não utilizados pelo System Center Configuration Manager. Por exemplo:  
> 
> 
> - Atributo: cn = MS-SMS--limites do Site  
>   -   Classe: cn = MS-SMS-Server--ponto de localização  

Pode certificar-se as listas anteriores estão atualizadas, visualizando o **ConfigMgr_ad_schema. LDF** ficheiro a partir de **\SMSSETUP\BIN\x64** pasta do suporte de dados de instalação do System Center Configuration Manager.  
