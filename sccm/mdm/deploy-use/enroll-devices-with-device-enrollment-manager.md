---
title: "Inscrever dispositivos com o Gestor de inscrição de dispositivos - Configuration Manager | Microsoft Docs"
description: "Inscreva dispositivos pertencentes à empresa com a conta de Gestor de inscrição de dispositivos com o System Center Configuration Manager."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
caps.latest.revision: "8"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: dcc35fb6ebe385d07a3b60e8968e06dec8ad60af
ms.sourcegitcommit: 40f2a4e3cc546e6bfd10f195a8e87af2b0780928
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/08/2017
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Inscrever dispositivos com o Gestor de inscrição de dispositivos com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As organizações podem utilizar o Intune para gerir um grande número de dispositivos móveis com uma única conta de utilizador. O *Gestor de inscrição de dispositivos* conta (DEM) é uma conta de utilizador especial utilizada para inscrever dispositivos. Adicionar utilizadores existentes para a conta DEM atribuir-lhes as capacidades DEM especiais. Cada dispositivo inscrito utiliza uma única licença. Recomendamos que utilize dispositivos inscritos através desta conta como dispositivos partilhados sem afinidade de utilizador, em vez de dispositivos pessoais e dedicados.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Inscrever dispositivos pertencentes à empresa com o Gestor de inscrição de dispositivos  
 Pode atribuir um Gestor de arquivo ou supervisor, por exemplo, um Gestor de inscrição de dispositivos conta de utilizador para permitir-lhe fazer o seguinte:  

-   Inscrever mais de 1000 dispositivos para gestão  
-   Utilizar a aplicação do Portal da empresa para instalar aplicações da empresa  
-   Configurar o acesso aos dados da empresa  

As seguintes limitações aplicam-se aos dispositivos geridos através de uma conta de Gestor de inscrição de dispositivos:

- O gerente da loja não é possível repor o dispositivo do portal da empresa.  
- Dispositivos não podem ser associada à área de trabalho ou associados ao Azure Active Directory. Isto impede que estes dispositivos utilizando o acesso condicional.
-  Para implementar aplicações da empresa em dispositivos geridos com o Gestor de inscrição de dispositivos, implementar a aplicação Portal da empresa, como um **instalação necessária** a conta de utilizador do Gestor de inscrição de dispositivos. O Gestor de inscrição de dispositivos, em seguida, pode iniciar a aplicação Portal da empresa para instalar aplicações adicionais.
- Para melhorar o desempenho, a aplicação Portal da empresa apenas mostra o dispositivo local. Gestão remota de outros dispositivos DEM só pode ser efetuada a partir da consola do Configuration Manager por e administrador
- O Web site do Portal da empresa não está disponível para contas de Gestor de inscrição de dispositivos. Utilize a aplicação do Portal da empresa.
- Se utilizar DEM para inscrever dispositivos iOS, não é possível utilizar o programa de inscrição de dispositivos da Apple (DEP) ou o Apple Configurator para inscrever dispositivos. (Apenas no iOS) 

 **Exemplos de cenários do Gestor de inscrição de dispositivos:**   
Um restaurante pretende obter tablets para a sua equipa de espera de mesa e monitores para os empregados da cozinha. Os empregados nunca precisam de aceder aos dados da empresa ou para iniciar sessão como um utilizador. O administrador do Intune cria uma conta de Gestor de inscrição de dispositivos e inscreve os dispositivos pertencentes à empresa através dessa conta. Em alternativa, o administrador poderia conceder a inscrição do dispositivo credenciais do Gestor a um Gestor de restaurante, permitindo-lhe ou a pessoa inscrever e gerir os dispositivos.  

 O administrador ou o gestor pode implementar aplicações de específicos da função para os dispositivos restaurante. Um administrador também pode selecionar um dispositivo na consola e extingui-lo da gestão de dispositivos móveis.  

#### <a name="add-a-device-enrollment-manager"></a>Adicionar um Gestor de inscrição de dispositivos  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. Selecione a subscrição do Microsoft Intune para o qual irá adicionar um Gestor de inscrição de dispositivos e, em seguida, clique em **propriedades**.  

3.  Na caixa de diálogo de propriedades de subscrição do Microsoft Intune, clique o **Gestor de inscrição de dispositivos** separador.  

4.  Clique em **Adicionar/remover**.  

5.  No **Gestor de inscrição de dispositivos** caixa de diálogo, escreva o nome de utilizador do utilizador que pretende adicionar como um Gestor de inscrição de dispositivos e, em seguida, clique em **pesquisa**. Selecione o utilizador que pretende adicionar como um Gestor de inscrição do dispositivo e clique em **adicionar**.  

6.  Confirme a conta de utilizador que será um Gestor de inscrição de dispositivos e clique em **Adicionar/remover**.  Uma licença de subscrição é necessária para cada utilizador que acede ao serviço e o *Gestor de inscrição de dispositivos* não pode ser um administrador do Intune. Determine se tem de adicionar mais licenças antes de utilizar esta funcionalidade.  

7.  O Gestor de inscrição de dispositivos pode agora inscrever dispositivos móveis utilizando o mesmo procedimento que utiliza um utilizador final para o cenário bring-your-own device (BYOD) no portal da empresa.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Eliminar um Gestor de inscrição de dispositivos do Intune  
Eliminar um Gestor de inscrição de dispositivos não afeta dispositivos inscritos. Quando é eliminado um Gestor de inscrição de dispositivos:  
- Dispositivos não inscritos são não inscritos  
- Os dispositivos inscritos continuam a ser completamente geridos  
- As credenciais de conta de Gestor de inscrição de dispositivos eliminada mantêm-se válidas para iniciar sessão no portal da empresa para acederem a aplicações  
- As credenciais de conta de Gestor de inscrição de dispositivos eliminada não é possível apagar ou extinguir dispositivos  
- Relação de dispositivos eliminada inscrição manager da conta para concluíram a inscrição de dispositivos permanecem mas não há dispositivos adicionais podem ser inscritos

1.  Na consola do Configuration Manager, clique em **Administração**.  
2.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. Selecione a subscrição do Microsoft Intune para o qual irá adicionar um Gestor de inscrição de dispositivos e, em seguida, clique em **propriedades**.  
3.  Na caixa de diálogo de propriedades de subscrição do Microsoft Intune, clique o **Gestor de inscrição de dispositivos** separador.  
4.  **Pesquisa** para o Gestor de inscrição de dispositivos que pretende eliminar e clique em **remover**, em seguida, **OK**.  
