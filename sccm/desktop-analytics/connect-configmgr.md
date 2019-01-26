---
title: Ligar o Configuration Manager
titleSuffix: Configuration Manager
description: Um guia de procedimentos para ligar o Configuration Manager com a análise de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 76ccac3c1c996d91f65e458f6e31e13783a26695
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073377"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Como ligar o Configuration Manager com a análise de ambiente de trabalho 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Análise de área de trabalho está totalmente integrado com o Configuration Manager. Primeiro, certifique-se de que o site é atualizado para suportar as funcionalidades mais recentes. Em seguida, crie a ligação de ambiente de trabalho de análise no Configuration Manager. Por fim, monitorize o estado de funcionamento da ligação. 


## <a name="bkmk_hotfix"></a> Atualizar o site

Primeiro, certifique-se de que seu site do Configuration Manager está em execução, pelo menos, versão 1810. Para obter mais informações, consulte [instalar atualizações na consola](/sccm/core/servers/manage/install-in-console-updates).

Também tem de instalar o rollup de atualização de versão 1810 (4486457) para suportar a integração com a análise de ambiente de trabalho. Para obter mais informações sobre esta atualização, consulte [Update rollup para o ramo atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4486457).

1. Atualize o site com o update rollup para a versão 1810. Para obter mais informações, consulte [instalar atualizações na consola](/sccm/core/servers/manage/install-in-console-updates).  

2. Atualize clientes. Para simplificar este processo, considere a utilização de atualização automática de cliente. Para obter mais informações, consulte [atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Ligar ao serviço

Utilize este procedimento para ligar o Configuration Manager para análise de ambiente de trabalho e configure as definições do dispositivo. Este procedimento é um processo único para anexar a hierarquia para o serviço em nuvem.  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **dos serviços do Azure** nó. Selecione **configurar os serviços do Azure** na faixa de opções.  

2. Sobre o **dos serviços do Azure** página do Assistente de serviços do Azure, configure as seguintes definições:  

    - Especifique um **nome** para o objeto no Configuration Manager.  

    - Especifique um opcional **Descrição** para ajudar a identificar o serviço.  

    - Selecione **Analytics de ambiente de trabalho** na lista de serviços disponíveis.  
  
   Selecione **Seguinte**.  

3. Sobre o **aplicação** , selecione o adequado **ambiente do Azure**. Em seguida, selecione **importação** para a aplicação web. Configure as seguintes definições no **importar aplicações** janela:  

    - **Nome de inquilino do Azure AD**: Este nome é como ele é chamado no Configuration Manager  

    - **ID de inquilino do Azure AD**: O **ID de diretório** que copiou do Azure AD   

    - **ID de cliente**: O **ID da aplicação** que copiou a partir da aplicação do Azure AD   

    - **Chave secreta**: A chave **valor** que copiou a partir da aplicação do Azure AD   

    - **Expiração da chave secreta**: A mesma data de expiração da chave   

    - **URI de ID de aplicação**: Esta definição deve preencher automaticamente com o seguinte valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **Verifique se**e, em seguida, selecione **OK** para fechar a janela de aplicações de importação. Selecione **seguinte** na página da aplicação do Assistente de serviços do Azure.  

4. Sobre o **dados de diagnóstico** página, configure as seguintes definições:  

    - **ID comercial**: este valor deve preencher automaticamente com o ID da sua organização  

    - **Nível de dados de diagnóstico do Windows 10**: selecione, pelo menos, **avançado (limitado)**  

    - **Permite que o nome de dispositivo em dados de diagnóstico**: selecione **ativar**  

        > [!Note]  
        > A partir do Windows 10 versão 1803, o nome do dispositivo não é enviado à Microsoft por predefinição. Se não tiver de enviar o nome do dispositivo, aparecerá na área de trabalho de análise como "Desconhecido". Esse comportamento pode tornar difícil identificar e avaliar os dispositivos.  

   Selecione **Seguinte**. O **funcionalidade disponível** página mostra a funcionalidade de análise de ambiente de trabalho que está disponível com as definições de dados de diagnóstico da página anterior. Selecione **próxima** para continuar ou **anterior** para fazer alterações.   

    ![Página de funcionalidade disponível de exemplo no Assistente de serviços do Azure](media/available-functionality.png)

5. Sobre o **coleções** página, configure as seguintes definições:  

    - **Nome a apresentar**: O portal de análise de ambiente de trabalho apresenta esta ligação do Configuration Manager com este nome. Usá-lo para diferenciar entre hierarquias diferentes. Por exemplo, *laboratório de teste* ou *produção*.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que configura o Configuration Manager com o seu ID comercial e as definições de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager liga-se para o serviço de análise de ambiente de trabalho.  

    - **Os dispositivos da coleção de destino utilizar um proxy de usuário autenticado para comunicações de saída**: Por predefinição, este valor é **não**. Se for necessário no seu ambiente, definido como **Sim**.   

    - **Selecione as coleções específicas para sincronizar com a análise de ambiente de trabalho**: Selecione **adicionar** para incluir coleções adicionais. Essas coleções estão disponíveis no portal do Analytics de ambiente de trabalho para o agrupamento com planos de implantação. Certifique-se incluir coleções de exclusão de piloto e piloto.  

        Essas coleções continuam a sincronizar como as alterações de associação. Por exemplo, o seu plano de implementação utiliza uma coleção com uma regra de associação do Windows 7. À medida que esses dispositivos atualizar para o Windows 10 e do Configuration Manager avalia a associação à coleção, esses dispositivos soltem fora de coleta e ao plano de implantação.  

6. Conclua o assistente.  

O Configuration Manager cria uma política de definições para configurar os dispositivos da coleção de destino. Esta política inclui as definições de dados de diagnóstico para permitir que os dispositivos enviar dados à Microsoft. Por predefinição, clientes de atualização de política de cada hora. Depois de receber as novas definições, pode ser mais de várias horas antes dos dados estão disponíveis no ambiente de trabalho de análise.



## <a name="bkmk_monitor"></a> Ligação de monitor do Estado de funcionamento

Monitorize a configuração dos seus dispositivos para análise de ambiente de trabalho. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **estado de funcionamento da ligação** dashboard.  

Para obter mais informações, consulte [monitorizar o estado de funcionamento da ligação](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

O Configuration Manager sincroniza os planos de implementação de análise de ambiente de trabalho em menos de 15 minutos a criar a ligação. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **planos de implantação** nó. 



## <a name="next-steps"></a>Passos seguintes

Avance para o artigo seguinte para inscrever dispositivos para análise de ambiente de trabalho.
> [!div class="nextstepaction"]  
> [Inscrever dispositivos](/sccm/desktop-analytics/enroll-devices)  

