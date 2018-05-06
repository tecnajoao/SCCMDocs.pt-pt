---
title: Definir limites
titleSuffix: Configuration Manager
description: Compreenda como definem localizações de rede na sua intranet que pode conter dispositivos que pretende gerir.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e27bce7576f6d96a8e8af95fa5df69dd39c05cd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="define-network-locations-as-boundaries-for-system-center-configuration-manager"></a>Definir localizações de rede como limites para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Limites de Gestor de configuração são localizações na sua rede que contém dispositivos que pretende gerir. O limite de que um dispositivo estiver numa é equivalente ao site do Active Directory ou o endereço IP de rede que é identificado pelo cliente Configuratoin Manager que está instalado no dispositivo.
 - Pode criar manualmente limites individuais. No entanto, o Configuration Manager não suporta a introdução direta de uma super-rede como um limite. Em vez disso, utilize o tipo de limite de intervalo de endereços IP.
 - Pode configurar o [deteção de floresta do Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) método para detetar automaticamente e criar limites para cada sub-rede IP e Site do Active Directory que Deteta. Quando a deteção de floresta do Active Directory identifica uma super-rede atribuída a um site do Active Directory, o Configuration Manager converte a Super-rede num limite de intervalo de endereços IP.  

Não é invulgar para um dispositivo utilizar um endereço IP que não tem conhecimento de administrador do Configuration Manager. Quando a localização de rede de um dispositivo está em dúvida, confirme que o dispositivo relata como localização, utilizando o **IPCONFIG** comando no dispositivo.  

Quando cria um limite, este recebe automaticamente um nome baseado no tipo e no âmbito do limite. Não é possível modificar este nome. Em vez disso, pode especificar uma descrição para ajudar a identificar o limite na consola do Configuration Manager.  

Cada limite está disponível para utilização por todos os sites na sua hierarquia. Depois de ter sido criado um limite, pode modificar as suas propriedades para fazer o seguinte:  
-   Adicionar o limite a um ou mais grupos de limites.  
-   Alterar o tipo ou o âmbito do limite.  
-   Consulte o separador **Sistemas de Sites** dos limites para verificar que servidores do sistema de sites (pontos de distribuição, pontos de migração de estado e pontos de gestão) estão associados ao limite.  

## <a name="to-create-a-boundary"></a>Para criar um limite  

1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** > **limites**  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Boundary**.  

3.  No separador **Geral** da caixa de diálogo Criar Limites, é possível especificar uma **Descrição** para identificar o limite através de um nome amigável ou de uma referência.  

4.  Selecione um **Tipo** para este limite:  

    -   Se selecionar **Sub-rede IP**, tem de especificar um **ID de Sub-rede** para este limite.  
        > [!TIP]  
        >  Pode especificar a **Rede** e a **Máscara de sub-rede** para que o **ID de Sub-rede** seja especificado automaticamente. Ao guardar o limite, apenas é guardado o valor do ID de Sub-rede.  

    -   Se selecionar **site do Active Directory**, tem de especificar ou **Procurar** um site do Active Directory na floresta local do servidor do site.  

        > [!IMPORTANT]  
        >  Quando especifica um site do Active Directory para um limite, o limite inclui cada Sub-rede de IP que é membro desse site do Active Directory. Se a configuração do site Active Directory for alterada no Active Directory, as localizações de rede incluídas neste limite também são alteradas.  

    -   Se selecionar **prefixo IPv6**, tem de especificar um **Prefixo** no formato de prefixo IPv6.  

    -   Se selecionar **Intervalo de endereços IP**, tem de especificar um **Endereço IP inicial** e um **Endereço IP final** que incluam parte de uma Sub-rede de IP ou várias Sub-redes IP.    

5.  Clique em **OK** para guardar o novo limite.  

## <a name="to-configure-a-boundary"></a>Para configurar um limite  

1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** > **limites**  

2.  Selecione o limite que pretende modificar.  

3.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** do limite, selecione o separador **Geral** para editar a **Descrição** ou o **Tipo** do limite. Também pode alterar o âmbito de um limite, editando as suas localizações de rede. Por exemplo, para o limite de um site do Active Directory, pode especificar um novo nome de site do Active Directory.  

5.  Selecione o separador **Sistemas de Sites** para visualizar os sistemas de sites associados a este limite. Não é possível alterar esta configuração a partir das propriedades de um limite.  

    > [!TIP]  
    >  Para que um servidor do sistema de sites seja apresentado como um sistema de sites para um limite, o servidor do sistema de sites tem de estar associado como um servidor do sistema de sites a, pelo menos, um grupo de limites que inclua este limite. Isto é configurado no separador **Referências** de um grupo de limites.  

6.  Selecione o separador **Grupos de Limites** para modificar a associação do grupo de limites para este limite:  

    -   Para adicionar este limite a um ou mais grupos de limites, clique em **Adicionar**, selecione a caixa de verificação de um ou mais grupos de limites e clique em **OK**.  

    -   Para remover este limite de um grupo de limites, selecione o grupo de limites e clique em **Remover**.  

7.  Clique em **OK** para fechar as propriedades do limite e guardar a configuração.  
