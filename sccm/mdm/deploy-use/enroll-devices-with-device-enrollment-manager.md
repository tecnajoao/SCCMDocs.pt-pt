---
title: "Inscrever dispositivos com o Gestor de inscrição de dispositivos - Configuration Manager | Documentos do Microsoft"
description: "Inscreva dispositivos pertencentes à empresa com a conta de Gestor de inscrição de dispositivos com o System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
caps.latest.revision: 8
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 7573590763c68a4c97d388be1e64054c318da9cc
ms.openlocfilehash: 8c491636925670732e6af67d8c1c741e4793ef96
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Inscrever dispositivos com o Gestor de inscrição de dispositivos com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As organizações podem utilizar o Intune para gerir um grande número de dispositivos móveis com uma conta de utilizador único. O *Gestor de inscrição de dispositivos* (DEM) é uma conta de utilizador especial que pode inscrever até 1000 dispositivos. Adicionar utilizadores existentes para a conta DEM dar-lhes as capacidades DEM especiais. Cada dispositivo inscrito utiliza uma única licença. Recomendamos que utilize os dispositivos inscritos através desta conta como dispositivos partilhados com nenhuma afinidade do utilizador, em vez de dispositivos pessoais e dedicados.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Inscrever dispositivos pertencentes à empresa com o Gestor de inscrição de dispositivos  
 Pode atribuir um arquivo ou supervisor de, por exemplo, um Gestor de inscrição de dispositivos conta de utilizador para permitir ao mesmo proceda da seguinte forma:  

-   Inscrever até 1000 dispositivos para gestão  
-   Utilizar a aplicação de Portal da empresa para instalar aplicações da empresa  
-   Configurar o acesso a dados da empresa  

As seguintes limitações aplicam-se aos dispositivos geridos através de uma conta de Gestor de inscrição de dispositivos:

- O gerente da loja não pode repor o dispositivo a partir do portal da empresa.  
- Dispositivos não podem ser associada à área de trabalho ou do Azure Active Directory associado. Isto impede o destes dispositivos e utilizar o acesso condicional.
-  Para implementar aplicações da empresa em dispositivos geridos com o Gestor de inscrição de dispositivos, implementar a aplicação de Portal da empresa como um **instalação necessária** à conta de utilizador do Gestor de inscrição de dispositivos. O Gestor de inscrição de dispositivos, em seguida, pode iniciar a aplicação Portal da empresa para instalar aplicações adicionais.
- Para melhorar o desempenho, a aplicação Portal da empresa mostra apenas o dispositivo local. Gestão remota de outros dispositivos DEM só pode ser efetuada a partir da consola do Configuration Manager por e administrador
- O site do Portal da empresa não está disponível para contas de Gestor de inscrição de dispositivos. Utilize a aplicação do Portal da empresa.
- (apenas iOS) Se utilizar DEM para inscrever dispositivos iOS, é possível utilizar o programa de inscrição de dispositivos da Apple (DEP) ou o Apple Configurator para inscrever dispositivos.

 **Exemplos de cenários do Gestor de inscrição de dispositivos:**   
Um restaurante pretende obter tablets para a equipa de espera e a ordem-monitores para os empregados da cozinha. Os empregados nunca precisam de aceder aos dados da empresa ou para iniciar sessão como um utilizador. O administrador do Intune cria uma conta de Gestor de inscrição de dispositivos e inscreve os dispositivos pertencentes à empresa através dessa conta. Em alternativa, o administrador pode conceder a inscrição de dispositivos credenciais de Gestor de Gestor do restaurante, que lhe permitirá inscrever e gerir os dispositivos.  

 O administrador ou gestor pode implementar aplicações específicas de função de dispositivos do restaurante. Um administrador também pode selecionar um dispositivo na consola e extingui-lo da gestão de dispositivos móveis.  

#### <a name="add-a-device-enrollment-manager"></a>Adicionar um Gestor de inscrição de dispositivos  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. Selecione a subscrição do Microsoft Intune para o qual irá adicionar um Gestor de inscrição de dispositivos e, em seguida, clique em **propriedades**.  

3.  Na caixa de diálogo Propriedades da subscrição do Microsoft Intune, clique a **Gestor de inscrição de dispositivos** separador.  

4.  Clique em **Adicionar/remover**.  

5.  No **Gestor de inscrição de dispositivos** caixa de diálogo, escreva o nome de utilizador do utilizador que pretende adicionar como um Gestor de inscrição de dispositivos e, em seguida, clique em **pesquisa**. Selecione o utilizador que pretende adicionar como um Gestor de inscrição do dispositivo e clique em **adicionar**.  

6.  Confirme a conta de utilizador que será um Gestor de inscrição de dispositivos e clique em **Adicionar/remover**.  É necessária para cada utilizador que aceda ao serviço uma licença de subscrição e o *Gestor de inscrição de dispositivos* não pode ser um administrador do Intune. Determine se precisa de adicionar mais licenças antes de utilizar esta funcionalidade.  

7.  O Gestor de inscrição de dispositivos agora pode inscrever dispositivos móveis com o mesmo procedimento utilizado pelo utilizador final para um cenário de bring-your-proprietário-device (BYOD) no portal da empresa.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Eliminar um Gestor de inscrição de dispositivos do Intune  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. Selecione a subscrição do Microsoft Intune para o qual irá adicionar um Gestor de inscrição de dispositivos e, em seguida, clique em **propriedades**.  

3.  Na caixa de diálogo Propriedades da subscrição do Microsoft Intune, clique a **Gestor de inscrição de dispositivos** separador.  

4.  **Pesquisa** para o Gestor de inscrição de dispositivos que pretende eliminar e clique em **remover**, em seguida, **OK**.  

 Eliminar um Gestor de inscrição de dispositivos não afeta os dispositivos inscritos. Quando um Gestor de inscrição de dispositivos é eliminado:  

-   Dispositivos inscritos não são afetados  

-   Os dispositivos inscritos continuam a ser completamente geridos  

-   As credenciais de conta de Gestor de inscrição de dispositivos eliminada mantêm-se válidas para iniciar sessão no portal da empresa para aceder a aplicações  

-   As credenciais de conta de Gestor de inscrição de dispositivos eliminada não é possível apagar ou extinguir dispositivos  

-   Relação de dispositivos eliminada inscrição manager da conta com os dispositivos permanecem inscritos, mas não inscrever mais dispositivos podem ser

