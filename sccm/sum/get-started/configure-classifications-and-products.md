---
title: "Configurar classificações e produtos para sincronizar | Microsoft Docs"
description: "Siga estes passos para configurar classificações e produtos para sincronizar na consola do Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 2da61e6e06850b36543b9fd41bd9a7d2368006fb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>Configurar classificações e produtos a sincronizar  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


> [!NOTE]  
>  Utilize o procedimento desta secção apenas no site de nível superior.  

 Os metadados de atualizações de software são obtidos durante o processo de sincronização no Configuration Manager com base nas definições que especificou nas propriedades do componente de ponto de atualização de Software. Depois de sincronizar as atualizações de software pela primeira vez, ou quando são lançadas novos produtos e classificações, tem de ir para as propriedades para selecionar os itens de novo. Utilize o seguinte procedimento para configurar classificações e produtos a sincronizar.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar classificações e produtos a sincronizar  

1.  No **do Configuration Manager** consola, navegue para **administração** > **configuração do Site** > **Sites**.

2. Selecione o site de administração central ou site primário autónomo.  

3.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.

4.  No separador **Classificações** , especifique as classificações de atualização de software para as quais quer sincronizar atualizações de software.  

    > [!NOTE]  
    >  Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualizações. Durante o processo de sincronização, serão sincronizados os metadados de atualizações de software para as classificações especificadas. O Configuration Manager fornece a capacidade para sincronizar atualizações de software com as seguintes classificações de atualização:  
    >   
    > - **Atualizações críticas**: Especifica uma atualização amplamente lançada para um problema específico que corrige um crítico não relacionado com segurança.  
    > - **As atualizações de definições**: Especifica uma atualização para vírus ou outros ficheiros de definição.  
    > - **Pacotes de funcionalidades**: Especifica as novas funcionalidades do produto que são distribuídas fora de uma versão de produto e que normalmente estão incluídas na próxima versão completa do produto.  
    > - **Atualizações de segurança**: Especifica uma atualização amplamente lançada para um problema específico do produto, relacionadas com segurança.  
    > - **Service Packs**: Especifica um conjunto cumulativo de correções que são aplicadas a uma aplicação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.  
    > - **Ferramentas**: Especifica um utilitário ou funcionalidade que ajuda a efetuar uma ou mais tarefas.  
    > - **Update Rollups**: Especifica um conjunto cumulativo de correções que são agrupadas para facilitar a implementação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um rollup de atualizações resolve geralmente uma área específica, tal como segurança ou um componente de produto.  
    > - **Atualizações**: Especifica uma atualização para uma aplicação ou um ficheiro que está atualmente instalado.  
    > - **Atualizar**: Especifica uma atualização para Windows 10 e funcionalidades. Os pontos de atualização de software e os sites têm de executar um mínimo de WSUS 4.0 com a [correção 3095113](https://support.microsoft.com/kb/3095113) para obter o **atualizar** classificação.    
    >       

    > [!NOTE]    
    > A partir do Configuration Manager versão 1706, também pode selecionar o **incluem o Microsoft Surface controladores e as atualizações de firmware** caixa de verificação para sincronizar controladores Microsoft Surface. Todos os pontos de atualização de software tem de executar para sincronizar com êxito a superfície controladores do Windows Server 2016.     
    >    
    > Esta é uma funcionalidade de pré-lançamento. As funcionalidades de pré-lançamento estão incluídas no produto para um teste antecipado num ambiente de produção, mas devem não ser consideradas prontas para produção. Tem de ativar esta funcionalidade para que fique disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

5.  No separador **Produtos** , especifique os produtos para os quais quer sincronizar atualizações de software e, em seguida, clique em **Fechar**.  

    > [!NOTE]  
    >  Os metadados para cada atualização de software definem os produtos para os quais a atualização é aplicável. Um produto é uma edição específica de um sistema operativo ou aplicação, como o Windows Server 2012. Uma família de produtos é o sistema operativo base ou a aplicação a partir da qual derivam os produtos individuais. Um exemplo de uma família de produtos é o Windows, do qual o Windows Server 2012 é membro. Pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos. Quantos mais produtos selecionar, mais tempo demorará para sincronizar atualizações de software.  
    >   
    >  Quando as atualizações de software sejam aplicam a vários produtos e pelo menos um dos produtos foi selecionado para sincronização, todos os produtos aparecerão na consola do Configuration Manager, mesmo se alguns produtos não foram selecionados. Por exemplo, se o Windows Server 2012 for o único sistema operativo que selecionou, e se uma atualização de software se aplicar ao Windows 8 e Windows Server 2012, ambos os produtos serão apresentados na consola do Configuration Manager.  

    > [!IMPORTANT]  
    >  O Configuration Manager armazena uma lista de produtos e famílias de produtos a partir dos quais pode escolher quando instalar pela primeira vez o software de um ponto de atualização. Produtos e famílias de produtos que são lançadas depois do Configuration Manager ser lançado poderão não estar disponíveis para seleção até concluir a sincronização de atualizações de software, que atualiza a lista de produtos disponíveis e famílias de produtos a partir da qual pode escolher.  

## <a name="next-steps"></a>Passos seguintes
Inicie a sincronização de atualizações de software para obter atualizações de software com base nos critérios de novo. Para obter mais informações, consulte [sincronizar atualizações de software](synchronize-software-updates.md).
