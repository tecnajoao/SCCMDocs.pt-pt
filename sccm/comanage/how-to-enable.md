---
title: Ativar a cogestão
titleSuffix: Configuration Manager
description: Ative rapidamente a cogestão no Configuration Manager para obter valor imediato.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37dce37551627394da2630fa591a3c803ae8343f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135776"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>Como ativar a cogestão no Configuration Manager

Quando ativar a cogestão, pode obter valor imediato. Em seguida, quando estiver pronto, pode começar a fazer a transição de cargas de trabalho conforme necessário no seu ambiente.

Certificar-se de que os pré-requisitos de cogestão são configurados antes de iniciar este processo. Para obter mais informações, consulte [pré-requisitos](/sccm/comanage/overview#prerequisites).



## <a name="process"></a>Processo

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó. Clique em **configurar cogestão** na faixa de opções para abrir o **Assistente de ativação da cogestão**.  

2. Sobre o **subscrição** página do assistente, selecione **sessão**. Inicie sessão no seu inquilino do Intune e, em seguida, selecione **seguinte**.  

3. Na **ativação** página, selecione seu **a inscrição automática no Intune** definir, optar por **piloto** ou **todos os**.   

    Esta ação permite a inscrição automática do cliente no Intune para clientes existentes do Configuration Manager. Quando escolhe **piloto**, apenas os clientes do Configuration Manager que são membros da coleção piloto são automaticamente inscritos no Intune. Esta opção permite-lhe ativar a cogestão num subconjunto de clientes para testar inicialmente cogestão e cogestão de implementação de forma faseada.  

    > [!Note]  
    > A partir da versão 1806, a inscrição automática não é imediata para todos os clientes. Este comportamento ajuda a escala de inscrição melhor para ambientes de grandes dimensões. O Configuration Manager a aleatorização de inscrição com base no número de clientes. Por exemplo, se o ambiente tiver 100.000 clientes, quando habilitar essa configuração, inscrição ocorre ao longo de vários dias.<!--1358003-->  

    Se tiver dispositivos baseados na internet que já tenham sido inscritos no Intune, copie a linha de comandos nesta página. Pode usar esta linha de comandos para instalar o cliente do Configuration Manager como uma aplicação no Intune.

4. Sobre o **cargas de trabalho** página, para cada carga de trabalho, escolher o grupo de dispositivos para mover-se através de gestão com o Intune. Para obter mais informações, consulte [cargas de trabalho](/sccm/comanage/workloads).  

    Se só quiser ativar a cogestão, não precisa de mudar as cargas de trabalho agora. Pode mudar as cargas de trabalho mais tarde. Para obter mais informações, consulte [como mudar as cargas de trabalho](/sccm/comanage/how-to-switch-workloads).  

    O **Intune piloto** definição muda a carga de trabalho associada apenas para os dispositivos na coleção piloto. O **Intune** definição muda a carga de trabalho associada para todos os dispositivos Windows 10 cogeridos.  

    > [!Important] 
    > Antes de alternar quaisquer cargas de trabalho, certifique-se de que configure corretamente e implementar a carga de trabalho correspondente no Intune. Certifique-se de que as cargas de trabalho são sempre gerenciadas por uma das ferramentas de gerenciamento para os seus dispositivos.  

5. Sobre o **teste** página, configure as seguintes definições:  

    - **Piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte da sua implementação faseada de cogestão. Começar com uma coleção de teste pequeno e, em seguida, adicione mais coleções no grupo piloto, como implementar a cogestão para obter mais utilizadores e dispositivos. Pode alterar as coleções no grupo piloto em qualquer altura.  

    - **Produção**: Configurar o **grupo de exclusão** com uma ou mais coleções. Dispositivos que são membros de qualquer uma das coleções deste grupo são excluídos da cogestão a utilizar.  

6. Para ativar a cogestão, conclua o assistente.  



## <a name="next-steps"></a>Passos seguintes

Agora que ativou a cogestão, veja os artigos seguintes para o valor imediato, pode obter no seu ambiente:

- [Acesso condicional](/sccm/comanage/quickstart-conditional-access)  

- [Ações remotas do Intune](/sccm/comanage/quickstart-remote-actions)  

- [Estado de funcionamento do cliente](/sccm/comanage/quickstart-client-health)  
