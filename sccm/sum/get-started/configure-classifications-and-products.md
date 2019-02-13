---
title: Configurar classificações e produtos
titleSuffix: Configuration Manager
description: Siga estes passos para configurar classificações de atualização de software e produtos para sincronizar na consola do Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d66d34cc6199176ed81329b7fa92c65d329d1f1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129260"
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>Configurar classificações e produtos para sincronizar  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


> [!NOTE]  
>  Utilize o procedimento desta secção apenas no site de nível superior.  

 Metadados de atualizações de software é obtido durante o processo de sincronização no Configuration Manager com base nas definições que especificou nas propriedades do componente de ponto de atualização de Software. Depois de sincronizar as atualizações de software pela primeira vez ou quando novos produtos e classificações são lançadas, é preciso ir para as propriedades para selecionar os novos itens. Utilize o seguinte procedimento para configurar classificações e produtos a sincronizar.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar classificações e produtos a sincronizar  

1.  Na **Configuration Manager** da consola, navegue até **administração** > **configuração do Site** > **Sites**.

2. Selecione o site de administração central ou site primário autónomo.  

3.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.

4.  No separador **Classificações** , especifique as classificações de atualização de software para as quais quer sincronizar atualizações de software.  

    > [!NOTE]  
    >  Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualizações. Durante o processo de sincronização, serão sincronizados os metadados de atualizações de software para as classificações especificadas. O Configuration Manager fornece a capacidade de sincronizar atualizações de software com as seguintes classificações de atualização:  
    >   
    > - **Atualizações críticas**: Especifica uma atualização amplamente lançada para um problema específico que corrige um erro crítico não relacionado com segurança.  
    > - **Atualizações de definições**: Especifica uma atualização para vírus ou outros ficheiros de definição.  
    > - **Pacotes de funcionalidades**: Especifica as novas funcionalidades do produto que são distribuídas fora de uma versão de produto e que normalmente estão incluídas na próxima versão completa do produto.  
    > - **Atualizações de segurança**: Especifica uma atualização amplamente lançada para um problema específico do produto, relacionadas com segurança.  
    > - **Service Packs**: Especifica um conjunto cumulativo de correções que são aplicadas a uma aplicação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.  
    > - **Ferramentas**: Especifica um utilitário ou funcionalidade que ajuda a efetuar uma ou mais tarefas.  
    > - **Rollups de atualizações**: Especifica um conjunto cumulativo de correções que são agrupadas para facilitar a implementação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um rollup de atualizações resolve geralmente uma área específica, tal como segurança ou um componente de produto.  
    > - **Atualizações**: Especifica uma atualização para uma aplicação ou ficheiro que está atualmente instalado.  
    > - **Atualizar**: Especifica uma atualização para funcionalidades do Windows 10. Seus sites e pontos de atualização de software tem de executar um mínimo de WSUS 4.0 com o [correção 3095113](https://support.microsoft.com/kb/3095113) para obter o **atualizar** classificação.    
    >       

    > [!NOTE]    
    > A partir do Configuration Manager versão 1706, pode selecionar o **drivers de incluir o Microsoft Surface e atualizações de firmware** caixa de verificação para sincronizar os controladores do Microsoft Surface.<!--1098490--> Todos os pontos de atualização de software devem executar o Windows Server 2016 para sincronizar com êxito os drivers de superfície. Se ativar um ponto de atualização de software num computador com o Windows Server 2012 depois de ativar os controladores de superfície, os resultados da análise para as atualizações de controladores não são precisos. Isso resulta em dados de conformidade incorreta apresentados na consola do Configuration Manager e nos relatórios do Configuration Manager.  
    >  
    > Esse recurso foi introduzido pela primeira vez na versão 1706 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1710, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  
    >  
    > O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

5.  No separador **Produtos** , especifique os produtos para os quais quer sincronizar atualizações de software e, em seguida, clique em **Fechar**.  

    > [!NOTE]  
    >  Os metadados para cada atualização de software definem os produtos para os quais a atualização é aplicável. Um produto é uma edição específica de um sistema operativo ou aplicação, como o Windows Server 2012. Uma família de produtos é o sistema operativo base ou a aplicação a partir da qual derivam os produtos individuais. Um exemplo de uma família de produtos é o Windows, do qual o Windows Server 2012 é membro. Pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos. Quantos mais produtos selecionar, mais tempo demorará a sincronização de atualizações de software.  
    >   
    >  Quando as atualizações de software se aplicam a vários produtos e, pelo menos um dos produtos foi selecionado para sincronização, todos os produtos aparecerão na consola do Configuration Manager, mesmo se alguns produtos não foram selecionados. Por exemplo, se o Windows Server 2012 é o único sistema operativo que selecionou, e se uma atualização de software se aplicar ao Windows 8 e Windows Server 2012, ambos os produtos são apresentados na consola do Configuration Manager.  

    > [!IMPORTANT]  
    >  Gestor de configuração armazena uma lista de produtos e famílias de produtos a partir da qual pode escolher quando instalar pela primeira vez o software de ponto de atualização. Produtos e famílias de produtos que são lançadas após o lançamento do Configuration Manager poderão não estar disponíveis para seleção até concluir a sincronização de atualizações de software, que atualiza a lista de produtos disponíveis e famílias de produtos a partir do qual pode escolha.  

## <a name="next-steps"></a>Passos seguintes
Inicie a sincronização de atualizações de software para obter atualizações de software com base nos critérios de novo. Para obter detalhes, consulte [sincronizar as atualizações de software](synchronize-software-updates.md).
