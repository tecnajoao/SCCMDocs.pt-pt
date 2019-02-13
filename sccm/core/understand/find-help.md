---
title: Encontrar ajuda
titleSuffix: Configuration Manager
description: Encontre recursos para obter mais informações sobre o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9c4b9bdbd67e26962a4de3ff66643f071339795
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139481"
---
# <a name="find-help-for-using-configuration-manager"></a>Encontrar ajuda para utilizar o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo disponibiliza as seções a seguir com vários recursos para encontrar ajuda para utilizar o Configuration Manager:  

- [Documentação do produto](#bkmk_Info)  

- [Comentários sobre produtos de partilha](#product-feedback)  

- [Siga o blog da Equipe do Configuration Manager](#BKMK_ProductGroupBlog)  

- [Opções de suporte e recursos da comunidade](#BKMK_SupportOptions)  

Para obter ajuda com a acessibilidade de produto, consulte [funcionalidades de acessibilidade](/sccm/core/understand/accessibility-features).  



##  <a name="bkmk_Info"></a> Documentação do produto  

Para acessar a documentação do produto mais recente, começa com o [índice de biblioteca](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Para obter sugestões sobre como pesquisar, fornecendo comentários e obter mais informações sobre como utilizar a documentação do produto, consulte [como utilizar os documentos](/sccm/core/understand/use-docs).  



<a name="product-feedback"></a>  

## <a name="BKMK_1806Feedback"></a> Comentários sobre o produto a partir da versão 1806

A partir do Configuration Manager versão 1806, pode enviar comentários sobre o produto diretamente a partir da consola. Se precisar de anexar registos, utilize [Hub de comentários](#BKMK_FeedbackHub). Pode efetuar os seguintes procedimentos: <!--1357542-->

  - **Enviar um sorriso**: Envie comentários sobre o que gostou.
  - **Enviar comentários negativos**: Envie comentários sobre o que não gostou.
  - **Enviar uma sugestão**: Leva-o para o [Web site do UserVoice](https://configurationmanager.uservoice.com/) para compartilhar sua ideia.

![Enviar comentários no Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile"></a>Enviar um sorriso

Enviar comentários sobre algo que gostou siga as instruções abaixo: 
1. No canto superior direito da consola, clique na cara sorridente. 
2. No menu pendente, selecione **enviar um sorriso**.
3. Utilize a caixa de texto para explicar aquilo de que gostou. 
4. Escolha se pretende partilhar o seu endereço de email e uma captura de ecrã. 
5. Clique em **enviar comentários**
     - Se não tiver conectividade à internet, clique em **guardar** na parte inferior. Siga as instruções no [enviar comentários que guardou para a submissão posterior](#BKMK_NoInternet) secção para enviar para a Microsoft. 

![Submeter o formulário de comentários no Configuration Manager 1806](media/1806-feedback-form.png)


### <a name="send-a-frown"></a>Enviar comentários negativos

Enviar comentários sobre algo que não gostou siga as instruções abaixo:

1. No canto superior direito da consola, clique na cara sorridente. 
2. No menu pendente, selecione **enviar comentários negativos**.
3. Utilize a caixa de texto para explicar o que não gostou. 
4. Escolha se pretende partilhar o seu endereço de email e uma captura de ecrã. 
5. Clique em **enviar comentários**
     - Se não tiver conectividade à internet, clique em **guardar** na parte inferior. Siga as instruções no [enviar comentários que guardou para a submissão posterior](#BKMK_NoInternet) secção para enviar para a Microsoft.  


### <a name="information-sent-with-feedback"></a>Informações enviadas com comentários
 
   - Informações de compilação do SO
   - ID de hierarquia do Configuration Manager
   - Informações de compilação do produto
   - Informação do idioma
   - Identificador de dispositivo 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId


### <a name="BKMK_NoInternet"></a> Enviar comentários que guardou para a submissão posterior

1. Clique em **salvar** na parte inferior a **fornecer comentários** janela. 
2. Guarde o ficheiro. zip. Se o computador local não tiver acesso à internet, copie o ficheiro para um computador de ligado à internet. 
3. Se for necessário, copie UploadOfflineFeedback.exe localizado em `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`
    - Para obter mais informações sobre a pasta CD. Latest, consulte [The CD. Pasta mais recente](../servers/manage/the-cd.latest-folder.md)

4. Num computador ligado à internet, abra uma linha de comandos. 
5. Execute o seguinte comando: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Opcionalmente, pode especificar o seguinte:
        -  `-t, --timeout` Tempo limite em segundos para enviar os dados. 0 é ilimitado. A predefinição é 30.
        - `-s --silent`  Sem Registro em log à consola (não é possível combinar com – verboso)
        - `-v, --verbose` O registo verboso para a consola (não é possível combinar com – silencioso) de saída
        - `--help` Exibe a tela de ajuda



##  <a name="BKMK_FeedbackHub"></a> Comentários sobre o produto para versões anteriores e 1802

Defeitos de produto de potencial de relatório através da [aplicação Hub de comentários](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporada para o Windows 10. Quando **adicionar novo comentário**, certifique-se de que selecionar o **Enterprise Management** categoria e, em seguida, escolha uma das seguintes subcategorias:
 - Cliente do Configuration Manager
 - Consola do Configuration Manager
 - Implementação do SO do Configuration Manager
 - Servidor do Configuration Manager

Continuar a utilizar o [página do UserVoice](https://configurationmanager.uservoice.com/) votar em ideias para novas funcionalidades no Configuration Manager.


##  <a name="BKMK_ProductGroupBlog"></a> Blog da Equipe do Configuration Manager  

Os parceiros e de engenharia do Configuration Manager, as equipes usam os [blogue Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) para lhe fornecer informações técnicas e outras novidades sobre o Configuration Manager e as tecnologias relacionadas. As nossas publicações no blogue completam a documentação do produto e as informações de suporte.  


##  <a name="BKMK_SupportOptions"></a> Opções de suporte e recursos da comunidade  

As hiperligações seguintes fornecem informações sobre as opções de suporte e os recursos da comunidade:  

-   [Suporte da Microsoft](https://aka.ms/cmcbsupport)  

-   [Comunidade do Configuration Manager: Guia de sobrevivência do System Center Configuration Manager (ramo atual)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Página de fóruns do Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
