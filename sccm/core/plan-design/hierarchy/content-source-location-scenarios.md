---
title: "Localização de origem do conteúdo | Documentos do Microsoft"
description: "Saiba mais sobre as definições do System Center Configuration Manager que permitem que os clientes de localizar conteúdo numa rede lenta."
ms.custom: na
ms.date: 1/3/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 7f2fd3e550c7dc1b27996dc309b53f74e8c865e9
ms.openlocfilehash: a823458dc3b891b1c32d1cb44a96e8cafd376ed5
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="content-source-location-scenarios-in-system-center-configuration-manager"></a>Cenários de localização de origem de conteúdo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes da versão 1610, o System Center Configuration Manager suportadas várias definições que serão combinados para definir como e onde os clientes localizarem conteúdo quando se encontram numa rede lenta. As combinações possíveis afetam a utilização de clientes de localização de conteúdo e se com êxito podem utilizar uma localização de contingência quando uma origem preferencial da origem de conteúdo não está disponível.  

> [!IMPORTANT]  
> **Se os sites executem versão 1511, 1602 ou 1606**, as informações deste tópico aplicam-se à sua infraestrutura. Consulte também [grupos de limites para versões 1511,1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) para informações que são específicas para grupos de limites com estas versões do Configuration Manager.
>
> **Se os seus sites executarem a versão 1610 ou posterior**, utilize as informações no [definir limites de site e os grupos de limites para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups) para compreender como os clientes localizam pontos de distribuição que possuem conteúdo disponível.





**As seguintes três definições definem o comportamento quando os clientes solicitam conteúdo:**

-  **Permitir a localização de origem de contingência para conteúdo** (ativado ou não ativada): Esta é uma opção que é possível ativar no **grupos de limites** separador de um ponto de distribuição. Isto permite que o cliente para utilizar um ponto de distribuição que esteja configurado como uma localização de contingência quando o conteúdo não está disponível num ponto de distribuição preferenciais.  

 - **Comportamento de implementação para a velocidade da ligação de rede**: Cada implementação estiver configurada com um dos comportamentos seguintes a utilizar quando a ligação ao ponto de distribuição é lenta:  

    -   **Transferência de conteúdo do ponto de distribuição e executá-la localmente**  

    -   **Não transferir conteúdo**: Esta opção só é utilizada quando um cliente utiliza uma localização de contingência para obter conteúdo.  

    A velocidade da ligação para um ponto de distribuição está configurada no **referências** separador de um grupo de limites e é específico a esse grupo de limites.  

 -  **Distribuição de pacotes a pedido** (para pontos de distribuição preferenciais): Isto é ativado quando selecionar a opção **distribuir o conteúdo do pacote para pontos de distribuição preferenciais** no **definições de distribuição** separador da folha de propriedades do pacote ou da aplicação. Quando ativada, esta opção direciona automaticamente copiar o conteúdo para um ponto de distribuição preferenciais que ainda não possui o conteúdo após um cliente solicita que o conteúdo a partir do ponto de distribuição com o Configuration Manager.  


 **Os seguintes requisitos aplicam-se a todos os cenários:**


-   O conteúdo está disponível num ponto de distribuição de contingência  

-   Pontos de distribuição estão online e acessível  


## <a name="scenario-1"></a>Cenário 1  
 Aplica-se quando existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferencial**  

-   **Permitir contingência**: Não está ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário.)  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferenciais que contêm o conteúdo.  

3.  O cliente transfere o conteúdo de um ponto de distribuição preferenciais da lista.  

## <a name="scenario-2"></a>Cenário 2  
 Existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferencial**  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não transferir conteúdo  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário.)  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferenciais e os pontos de distribuição de contingência que têm o conteúdo.  

3.  O cliente transfere o conteúdo de um ponto de distribuição preferenciais da lista.  

## <a name="scenario-3"></a>Cenário 3  
 Existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferencial**  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Transferir e instalar conteúdo  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário.)  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferenciais e os pontos de distribuição de contingência que têm o conteúdo.  

3.  O cliente transfere o conteúdo de um ponto de distribuição preferenciais da lista.  

## <a name="scenario-4"></a>Cenário de 4  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** não está ativado  

-   **Permitir contingência**: Não está ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo. Não existem sem pontos de distribuição preferenciais na lista.  

3.  O cliente falha apresentando a mensagem **conteúdo não está disponível** e entra no modo de repetição. Um novo pedido de conteúdo é iniciado a cada hora.  

## <a name="scenario-5"></a>Cenário 5  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** não está ativado  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não transferir conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferenciais e os pontos de distribuição de contingência que possuem o conteúdo. Existirem pontos de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, uma tem o conteúdo.  

3.  O conteúdo não é transferido porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **não transferir conteúdo** (que é utilizado quando os clientes reverter para obter os conteúdos). O cliente falha apresentando a mensagem **conteúdo não está disponível** e entra no modo de repetição. O cliente faz um novo pedido de conteúdo a cada hora.  

## <a name="scenario-6"></a>Cenário 6  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** não está ativado  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Transferir e instalar conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que os pontos de distribuição de contingência estão ativados.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferenciais e os pontos de distribuição de contingência que possuem o conteúdo. Existem sem pontos de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, um que tenha o conteúdo.  

3.  O conteúdo é transferido a partir de um ponto de distribuição de contingência da lista porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **transferir e instalar o conteúdo**.  

## <a name="scenario-7"></a>Cenário 7  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** está ativada  

-   **Permitir contingência**: Não está ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo. Não existem sem pontos de distribuição preferidos que possuem o conteúdo.  

3.  O cliente falha apresentando a mensagem **conteúdo não está disponível** e entra no modo de repetição. Um novo pedido de conteúdo é efetuado a cada hora.  

4.  O ponto de gestão cria um acionador para o Gestor de distribuição distribua o conteúdo por todos os pontos de distribuição preferidos para o cliente que efetuou o pedido de conteúdo.  

5.  O Distribution Manager distribui o conteúdo por todos os pontos de distribuição preferenciais. Na maioria dos casos, o conteúdo é distribuído com êxito aos pontos de distribuição preferenciais no prazo uma hora.  

6.  Um novo pedido de conteúdo é iniciado pelo cliente ao ponto de gestão.  

7.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo. O cliente transfere o conteúdo de um ponto de distribuição preferenciais da lista.  

## <a name="scenario-8"></a>Cenário de 8  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** está ativada  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não transferir conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferenciais e os pontos de distribuição de contingência que possuem o conteúdo. Existirem pontos de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, uma tem o conteúdo.  

3.  O conteúdo não é transferido porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **não transferir**. O cliente falha apresentando a mensagem **conteúdo não está disponível** e entra no modo de repetição. O cliente faz um novo pedido de conteúdo a cada hora.  

4.  O ponto de gestão cria um acionador para o Gestor de distribuição distribua o conteúdo por todos os pontos de distribuição preferidos para o cliente que efetuou o pedido de conteúdo.  

5.  O Distribution Manager distribui o conteúdo por todos os pontos de distribuição preferenciais. Na maioria dos casos, o conteúdo é distribuído com êxito aos pontos de distribuição preferenciais no prazo uma hora.  

6.  Um novo pedido de conteúdo é iniciado pelo cliente ao ponto de gestão.  

7.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que possuem o conteúdo.  

8.  O cliente transfere o conteúdo de um ponto de distribuição preferenciais da lista.  

## <a name="scenario-9"></a>Cenário 9  
 Existem as seguintes configurações:  

-   **Conteúdo não está disponível num ponto de distribuição preferencial**  

-   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais** está ativada  

-   **Permitir contingência**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Transferir e instalar conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo ao ponto de gestão. O cliente inclui um sinalizador no pedido que indica que são permitidos pontos de distribuição de contingência.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferenciais e os pontos de distribuição de contingência que possuem o conteúdo. Existirem pontos de distribuição preferidos que possuem o conteúdo, mas o ponto de distribuição de contingência, pelo menos, uma tem o conteúdo.  

3.  O conteúdo é transferido a partir de um ponto de distribuição de contingência da lista porque a propriedade de implementação para quando o cliente utiliza um ponto de distribuição de contingência está definida como **transferir e instalar o conteúdo**. Esta definição de implementação permite que um cliente que tem de utilizar uma localização de conteúdo de contingência para obter os conteúdos a partir dessa localização.  

4.  O ponto de gestão cria um acionador para o Gestor de distribuição distribua o conteúdo por todos os pontos de distribuição preferidos para o cliente que efetuou o pedido de conteúdo.  

5.  O Distribution Manager distribui o conteúdo por todos os pontos de distribuição preferenciais, que permite que os clientes adicionais obter os conteúdos sem utilizar um ponto de distribuição de contingência.  

