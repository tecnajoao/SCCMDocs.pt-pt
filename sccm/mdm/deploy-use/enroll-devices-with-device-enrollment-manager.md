---
title: 'Inscrever dispositivos com o Gestor de inscrição de dispositivos '
titleSuffix: Configuration Manager
description: Inscreva dispositivos pertencentes à empresa com a conta de Gestor de inscrição de dispositivos com o System Center Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc1be1d602c3f9f8e65e0523d64c5b6a8e579c90
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415557"
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Inscrever dispositivos com o Gestor de inscrição de dispositivos com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As organizações podem utilizar o Intune para gerir um grande número de dispositivos móveis com uma conta de utilizador único. O *Gestor de inscrição de dispositivos* conta (DEM) é uma conta de utilizador especial utilizada para inscrever dispositivos. Pode adicionar utilizadores existentes à conta DEM para lhes capacidades especiais de DEM. Cada dispositivo inscrito utiliza uma única licença. Recomendamos que utilize dispositivos inscritos através desta conta como dispositivos partilhados sem afinidade de utilizador, em vez de dispositivos pessoais e dedicados.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Inscrever dispositivos pertencentes à empresa com o Gestor de inscrição de dispositivos  
 Pode atribuir um gerente da loja ou supervisor, por exemplo, um Gestor de inscrição de dispositivos conta de utilizador para conceder-lhe fazer o seguinte:  

-   Inscrever até 1000 dispositivos para gestão  
-   Utilizar a aplicação do Portal da empresa para instalar aplicações da empresa  
-   Configurar o acesso a dados da empresa  

As seguintes limitações aplicam-se a dispositivos geridos com uma conta de Gestor de inscrição de dispositivos:

- O gerente da loja não pode repor o dispositivo do portal da empresa.  
- Dispositivos não podem ser associada à área de trabalho ou associados ao Azure Active Directory. Isto impede que estes dispositivos através do acesso condicional.
- Para implementar aplicações da empresa em dispositivos geridos com o Gestor de inscrição de dispositivos, implemente a aplicação Portal da empresa como um **instalação necessária** a conta de utilizador do Gestor de inscrição de dispositivos. O Gestor de inscrição de dispositivos, em seguida, pode iniciar a aplicação Portal da empresa para instalar aplicações adicionais.
- Para melhorar o desempenho, a aplicação Portal da empresa mostra apenas no dispositivo local. Gestão remota de outros dispositivos DEM só pode ser efetuada a partir da consola do Configuration Manager por e administrador
- O site do Portal da empresa não está disponível para contas de Gestor de inscrição de dispositivos. Utilize a aplicação do Portal da empresa.
- Se utiliza DEM para inscrever dispositivos iOS, não é possível utilizar o Apple Configurator nem o programa de inscrição de dispositivos (DEP) da Apple para inscrever dispositivos. (Apenas no iOS) 

  **Exemplos de cenário do Gestor de inscrição de dispositivos:**   
  Um restaurante pretende obter tablets de sua equipe de espera de mesa e monitores para seus empregados da cozinha. Os empregados nunca precisam de aceder aos dados da empresa ou iniciar sessão como um utilizador. O administrador do Intune cria uma conta de Gestor de inscrição de dispositivos e inscreve os dispositivos pertencentes à empresa através dessa conta. Em alternativa, o administrador pode conceder a inscrição de dispositivos credenciais de gestor ao Gestor do restaurante, permitindo que ele ou ela inscrever e gerir os dispositivos.  

  O administrador ou gestor pode implementar aplicações específicas de funções para os dispositivos do restaurante. Um administrador também pode selecionar um dispositivo na consola e extingui-lo da gestão de dispositivos móveis.  

#### <a name="add-a-device-enrollment-manager"></a>Adicionar um gestor de inscrição de dispositivos  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. Selecione a subscrição do Microsoft Intune para o qual irá adicionar um Gestor de inscrição de dispositivos e, em seguida, clique em **propriedades**.  

3.  Na caixa de diálogo de propriedades de subscrição do Microsoft Intune, clique a **Gestor de inscrição de dispositivos** separador.  

4.  Clique em **Adicionar/remover**.  

5.  Na **Gestor de inscrição de dispositivos** caixa de diálogo, escreva o nome de utilizador do utilizador que pretende adicionar como um Gestor de inscrição de dispositivos e, em seguida, clique em **pesquisa**. Selecione o utilizador que pretende adicionar como um Gestor de inscrição do dispositivo e clique em **adicionar**.  

6.  Confirme a conta de utilizador que será um Gestor de inscrição de dispositivos e clique em **Adicionar/remover**.  Uma licença de subscrição é necessária para cada utilizador que acede ao serviço e o *Gestor de inscrição de dispositivos* não pode ser um administrador do Intune. Determine se é preciso adicionar mais licenças antes de utilizar esta funcionalidade.  

7.  O Gestor de inscrição de dispositivos agora pode inscrever dispositivos móveis com o mesmo procedimento que um utilizador final utiliza para um cenário de bring-your-own device (BYOD) no portal da empresa.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Eliminar um Gestor de inscrição de dispositivos do Intune  
A eliminar um Gestor de inscrição de dispositivos não afeta os dispositivos inscritos. Quando é eliminado um Gestor de inscrição de dispositivos:  
- Os dispositivos inscritos não são não inscritos  
- Os dispositivos inscritos continuam a ser completamente geridos  
- As credenciais de conta de Gestor de inscrição de dispositivos eliminada mantêm-se válidas para iniciar sessão no portal da empresa para aceder a aplicações  
- As credenciais de conta de Gestor de inscrição de dispositivos eliminada não é possível apagar ou extinguir dispositivos  
- Relação do dispositivo eliminado inscrição da conta do gestor para os inscritos é mantida de dispositivos, mas não existem dispositivos adicionais podem ser inscritos

1.  Na consola do Configuration Manager, clique em **Administração**.  
2.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. Selecione a subscrição do Microsoft Intune para o qual irá adicionar um Gestor de inscrição de dispositivos e, em seguida, clique em **propriedades**.  
3.  Na caixa de diálogo de propriedades de subscrição do Microsoft Intune, clique a **Gestor de inscrição de dispositivos** separador.  
4.  **Pesquisa** para o Gestor de inscrição de dispositivos que pretende eliminar e clique em **remover**, em seguida, **OK**.  
