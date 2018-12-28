---
title: Rever e substituir aplicações
titleSuffix: Configuration Manager
description: Saiba como trabalhar com versões de aplicações do System Center Configuration Manager e substituir aplicações.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b42012bdd6eb0456d25f9970ed2cf18f881a1c14
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424821"
---
# <a name="revise-and-supersede-applications-in-system-center-configuration-manager"></a>Rever e substituir aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Neste tópico, irá aprender como trabalhar com versões de aplicações do System Center Configuration Manager e como substituir aplicações com uma nova versão.  

##  <a name="application-revisions"></a>Revisões de aplicações  
 Quando são efetuadas revisões de uma aplicação ou para um tipo de implementação que está contido num aplicativo, o Configuration Manager cria uma nova revisão da aplicação. É possível visualizar o histórico de cada revisão da aplicação. Também é possível ver as suas propriedades, restaurar uma revisão anterior de uma aplicação ou eliminar uma revisão antiga.  

### <a name="to-display-an-application-revision-history"></a>Para visualizar um histórico de revisão da aplicação  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicativos**e, em seguida, escolha o aplicação que pretende.  

3.  Na **home page** separador a **aplicativo** de grupo, escolha **histórico de revisão** para abrir o **histórico de revisão da aplicação** caixa de diálogo.  

### <a name="to-view-an-application-revision"></a>Para visualizar uma revisão da aplicação  

1.  Na **histórico de revisão da aplicação** caixa de diálogo, selecione uma revisão da aplicação e, em seguida, escolha **vista**.  

2.  Na caixa de diálogo **Propriedades** , examine as propriedades da aplicação selecionada.  

    > [!NOTE]  
    >  As propriedades da aplicação que são apresentadas são só de leitura.  

3.  Feche a caixa de diálogo **Propriedades** .  

### <a name="to-restore-an-application-revision"></a>Para restaurar uma revisão da aplicação  

1.  Na **histórico de revisão da aplicação** caixa de diálogo, selecione uma revisão da aplicação e, em seguida, escolha **restaurar**.  

2.  Na **Confirmar restauro da revisão** caixa de diálogo caixa, escolha **Sim** para restaurar a revisão da aplicação selecionada.  

### <a name="to-delete-an-application-revision"></a>Para eliminar uma revisão da aplicação  

1.  Na **histórico de revisão da aplicação** caixa de diálogo, selecione uma revisão da aplicação e, em seguida, escolha **eliminar**.  

2.  Na **eliminar revisão da aplicação** caixa de diálogo caixa, escolha **Sim**.  

> [!IMPORTANT]  
>  Só é possível eliminar a revisão da aplicação atual se a aplicação estiver retirada e tem sem referências.  

##  <a name="application-supersedence"></a>Substituição de aplicações  
 Gestão de aplicações no Configuration Manager permite-lhe atualizar ou substituir as aplicações existentes utilizando uma relação de substituição. Quando uma aplicação é substituída, pode especificar um novo tipo de implementação para substituir o tipo de implementação da aplicação substituída e também decidir se atualizar ou desinstalar a aplicação substituída antes da aplicação substituta está instalado.  

> [!IMPORTANT]  
>  Quando é selecionada a opção para desinstalar o tipo de implementação substituído, não é possível substituir um tipo de implementação por outro que foi implementado num tipo de coleção diferente.  Por exemplo, um tipo de implementação que foi implementado numa coleção de dispositivos não pode ser substituído por um tipo de implementação que foi implementado numa coleção de utilizadores se a opção para desinstalar o tipo de implementação substituído estiver selecionada.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Decidir se é melhor atualizar ou substituir uma aplicação  
 O utilizador especifica se quer atualizar ou substituir uma aplicação na caixa de diálogo **Especificar Relação de Substituição** das propriedades da aplicação. O tipo de substituição depende se seleciona a opção **Desinstalar** na caixa de diálogo:  

-   Se pretende atualizar para uma versão mais recente da mesma aplicação (com o mesmo ID de aplicação), **isso não é possível** verificar **desinstalação**.  

-   Se pretende alterar para uma aplicação diferente (com um ID de aplicação diferente), selecione **Desinstalar**. Tem de remover a versão de substituição da aplicação.  

### <a name="supersede-dependent-applications"></a>Substituir aplicações dependentes  
 Neste exemplo, **aplicação global** refere-se para a aplicação que está a implementar que tem as dependências.  

 Pode criar uma relação de substituição que atualize a aplicação dependente para uma nova versão.  

1. Certifique-se de que a nova aplicação dependente e a aplicação dependente estão no mesmo grupo de dependência da aplicação global.  

2. Crie uma relação de substituição que substitua a aplicação dependente original pela nova aplicação dependente.  

   Durante as novas instalações da aplicação global, a nova aplicação dependente está instalada. As instalações existentes da aplicação global são atualizadas com a nova aplicação dependente.  

   O resultado final é que todas as implementações da aplicação global usar a nova aplicação dependente.  

### <a name="further-considerations"></a>Considerações adicionais  

-   Pode especificar múltiplas relações de substituição para aplicações dependentes. A aplicação dependente na localização superior na cadeia de substituição será a aplicação instalada.  

-   Aplicações dependentes tem de ser implementadas no dispositivo em que a aplicação global está instalada ou a aplicação dependente não é instalada.  

-   Para novas instalações da aplicação global, se tiver múltiplas dependências, a ordem da dependência determina qual a versão da aplicação dependente que é instalada.  

### <a name="to-specify-a-supersedence-relationship"></a>Para especificar uma relação de substituição  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicativos**e, em seguida, escolha o aplicação que substitui outra aplicação.  

3.  Sobre o **home page** separador o **propriedades** de grupo, escolha **propriedades** para abrir o nome da aplicação **propriedades** caixa de diálogo.  

4.  Sobre o **substituição** separador do *< nome da aplicação\>*  **propriedades** caixa de diálogo caixa, escolha **adicionar**.  

5.  Na caixa de diálogo **Especificar Relação de Substituição** , clique em **Procurar**.  

6.  Na **escolher aplicação** caixa de diálogo caixa, escolha a aplicação que pretende substituir e, em seguida, escolha **OK**.  

7.  Na **especificar relação de substituição** caixa de diálogo, selecione o tipo de implementação que substitui a implementação do tipo da aplicação substituída.  

    > [!NOTE]  
    >  Por predefinição, o novo tipo de implementação não desinstale o tipo de implementação da aplicação substituída. Este cenário é utilizado normalmente quando se pretende implementar uma atualização numa aplicação existente. Selecione **Desinstalar** para remover o tipo de implementação existente antes da instalação do novo tipo de implementação. Se optar por atualizar uma aplicação, certifique-se de que testa primeiro este procedimento num ambiente de laboratório.  

8.  Escolher **OK** para fechar a **especificar relação de substituição** caixa de diálogo.  

9. Escolha **OK** para fechar o *< nome da aplicação\>* **propriedades** caixa de diálogo.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Para apresentar as aplicações que substituem a aplicação atual  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software**.  

2.  Na **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**, escolha **aplicativos**e, em seguida, escolha a aplicação que pretende.  

3.  Na **home page** separador a **propriedades** de grupo, escolha **propriedades** para abrir o *< nome da aplicação\>*   **Propriedades** caixa de diálogo.  

4.  Sobre o **referências** separador do *< nome da aplicação\>*  **propriedades** caixa de diálogo caixa, escolha **aplicações que substituem esta aplicativo** partir de **tipo de relação** na lista pendente.  

5.  Reveja a lista de aplicações que substituem a aplicação selecionada e, em seguida, escolha **OK** para fechar a *< nome da aplicação\>*  **propriedades** caixa de diálogo.  
