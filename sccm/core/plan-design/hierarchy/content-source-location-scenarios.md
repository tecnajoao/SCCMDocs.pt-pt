---
title: Localização de origem de conteúdo
titleSuffix: Configuration Manager
description: Saiba mais sobre as definições do System Center Configuration Manager que permitem aos clientes localizar conteúdo numa rede lenta.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd80955f65b9c18ca0e2ed74e47caecb0e826049
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129175"
---
# <a name="content-source-location-scenarios-in-system-center-configuration-manager"></a>Cenários de localização de origem de conteúdo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Anterior à versão 1610, o System Center Configuration Manager suportadas várias configurações que combinados para definir como e onde os clientes localizam os conteúdos quando se encontram numa rede lenta. As combinações possíveis afetam a utilização de clientes de localização de conteúdo e, se este pode com êxito utilizar uma localização de contingência quando uma origem preferencial da origem para o conteúdo não está disponível.  

> [!IMPORTANT]  
> **Se os sites executarem a versão 1511, versão 1602 ou 1606**, as informações deste tópico aplica-se à sua infraestrutura. Consulte também [grupos de limites para versões 1511,1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) para informações específicas a grupos de limites com essas versões do Configuration Manager.
>
> **Se os sites executarem a versão 1610 ou posterior**, utilize as informações no [definir limites de site e grupos de limites para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups) para compreender como os clientes localizam os pontos de distribuição que tenham conteúdo disponível.





**As seguintes três definições definem o comportamento quando os clientes solicitam conteúdo:**

- **Permitir a localização de origem de contingência para conteúdo** (ativada ou não ativado): Esta é uma opção que pode ativar no **grupos de limites** separador de um ponto de distribuição. Isso permite que o cliente para utilizar um ponto de distribuição que está configurado como uma localização de contingência quando o conteúdo não está disponível num ponto de distribuição preferenciais.  

  - **Comportamento de implementação para a velocidade de ligação de rede**: Cada implementação está configurada com um dos seguintes comportamentos para utilizar quando a ligação ao ponto de distribuição é lenta:  

    -   **Transferir o conteúdo do ponto de distribuição e executá-lo localmente**  

    -   **Não transferir conteúdo**: Esta opção só é utilizada quando um cliente utiliza uma localização de contingência para obter conteúdo.  

    A velocidade da ligação para um ponto de distribuição está configurada no **referências** separador de um grupo de limites e é específico para esse grupo de limites.  

  - **Distribuição de pacotes a pedido** (para pontos de distribuição preferenciais): Esta opção estiver ativada quando seleciona a opção **distribuir o conteúdo do pacote para pontos de distribuição preferenciais** sobre o **definições de distribuição** separador de propriedades do pacote ou da aplicação. Quando ativada, esta opção direciona o Configuration Manager para copiar o conteúdo automaticamente para um ponto de distribuição preferencial que ainda não tem o conteúdo após um cliente solicita esse conteúdo a partir desse ponto de distribuição.  


 **Os seguintes requisitos de aplicam a todos os cenários:**


-   O conteúdo está disponível num ponto de distribuição de contingência  

-   Pontos de distribuição estão online e acessível  


## <a name="scenario-1"></a>Cenário 1  
 Aplica-se quando existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferencial**  

-   **Permitir contingência**: Não ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário).  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferenciais que contêm o conteúdo.  

3.  O cliente transfere o conteúdo a partir de um ponto de distribuição preferenciais na lista.  

## <a name="scenario-2"></a>Cenário 2  
 Existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferencial**  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não transferir conteúdo  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário).  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferenciais e pontos de distribuição de contingência que contêm o conteúdo.  

3.  O cliente transfere o conteúdo a partir de um ponto de distribuição preferenciais na lista.  

## <a name="scenario-3"></a>Cenário 3  
 Existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferencial**  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Transferir e instalar conteúdo  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário).  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferenciais e pontos de distribuição de contingência que contêm o conteúdo.  

3.  O cliente transfere o conteúdo a partir de um ponto de distribuição preferenciais na lista.  

## <a name="scenario-4"></a>Cenário de 4  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** não está ativada  

-   **Permitir contingência**: Não ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo. Não há nenhum ponto de distribuição preferenciais na lista.  

3.  O cliente falha apresentando a mensagem **conteúdo não está disponível** e entram em modo de repetição. Um novo pedido de conteúdo é iniciado a cada hora.  

## <a name="scenario-5"></a>Cenário 5  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** não está ativada  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não transferir conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferenciais e pontos de distribuição de contingência que possuem o conteúdo. Não há nenhum ponto de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, uma tem o conteúdo.  

3.  O conteúdo não é transferido porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **não transferir conteúdo** (que é utilizado quando os clientes utilizam para obter os conteúdos). O cliente falha apresentando a mensagem **conteúdo não está disponível** e entram em modo de repetição. O cliente faz um novo pedido de conteúdo a cada hora.  

## <a name="scenario-6"></a>Cenário 6  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** não está ativada  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Transferir e instalar conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que os pontos de distribuição de contingência estão ativados.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferenciais e pontos de distribuição de contingência que possuem o conteúdo. Existem não existem pontos de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, um que tenha o conteúdo.  

3.  O conteúdo é transferido a partir de um ponto de distribuição de contingência da lista porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **transferir e instalar o conteúdo**.  

## <a name="scenario-7"></a>Cenário 7  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** está ativada  

-   **Permitir contingência**: Não ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo. Não há nenhum ponto de distribuição preferidos que possuem o conteúdo.  

3.  O cliente falha apresentando a mensagem **conteúdo não está disponível** e entram em modo de repetição. Um novo pedido de conteúdo é feito a cada hora.  

4.  O ponto de gestão cria um acionador para o Gestor de distribuição para distribuir o conteúdo por todos os pontos de distribuição preferencial para o cliente que efetuou o pedido de conteúdo.  

5.  O Distribution Manager distribui o conteúdo por todos os pontos de distribuição preferenciais. Na maioria dos casos, o conteúdo é distribuído com êxito para os pontos de distribuição preferenciais dentro de uma hora.  

6.  Um novo pedido de conteúdo é iniciado pelo cliente para o ponto de gestão.  

7.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo. O cliente transfere o conteúdo a partir de um ponto de distribuição preferenciais na lista.  

## <a name="scenario-8"></a>Cenário de 8  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** está ativada  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não transferir conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferenciais e pontos de distribuição de contingência que possuem o conteúdo. Não há nenhum ponto de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, uma tem o conteúdo.  

3.  O conteúdo não é transferido porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **não transferir**. O cliente falha apresentando a mensagem **conteúdo não está disponível** e entram em modo de repetição. O cliente faz um novo pedido de conteúdo a cada hora.  

4.  O ponto de gestão cria um acionador para o Gestor de distribuição para distribuir o conteúdo por todos os pontos de distribuição preferencial para o cliente que efetuou o pedido de conteúdo.  

5.  O Distribution Manager distribui o conteúdo por todos os pontos de distribuição preferenciais. Na maioria dos casos, o conteúdo é distribuído com êxito para os pontos de distribuição preferenciais dentro de uma hora.  

6.  Um novo pedido de conteúdo é iniciado pelo cliente para o ponto de gestão.  

7.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo.  

8.  O cliente transfere o conteúdo a partir de um ponto de distribuição preferenciais na lista.  

## <a name="scenario-9"></a>Cenário de 9  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** está ativada  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Transferir e instalar conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente do ponto de gestão com os pontos de distribuição preferenciais e pontos de distribuição de contingência que possuem o conteúdo. Não há nenhum ponto de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, uma tem o conteúdo.  

3.  O conteúdo é transferido a partir de um ponto de distribuição de contingência da lista porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **transferir e instalar o conteúdo**. Esta definição de implementação permite que um cliente que têm de utilizar uma localização de conteúdo de contingência para obter os conteúdos a partir dessa localização.  

4.  O ponto de gestão cria um acionador para o Gestor de distribuição para distribuir o conteúdo por todos os pontos de distribuição preferencial para o cliente que efetuou o pedido de conteúdo.  

5.  O Distribution Manager distribui o conteúdo por todos os pontos de distribuição preferenciais, que permite que clientes adicionais obtenham o conteúdo sem utilizar um ponto de distribuição de contingência.  
