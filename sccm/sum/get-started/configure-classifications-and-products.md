---

title: "Configurar classificações e produtos a sincronizar | Documentos do Microsoft"
description: "Siga estes passos para configurar classificações e produtos a sincronizar na consola do Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.translationtype: Machine Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 6add66e625c790b65edf64216c2262a5d082f820
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017



---
#  <a name="configure-classifications-and-products-to-synchronize"></a>Configurar classificações e produtos a sincronizar  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


> [!NOTE]  
>  Utilize o procedimento desta secção apenas no site de nível superior.  

 Metadados de atualizações de software são obtidos durante o processo de sincronização no Configuration Manager com base nas definições que especificou nas propriedades do componente de ponto de atualização de Software. Depois de sincronizar as atualizações de software pela primeira vez, ou quando são lançadas novos produtos e classificações, tem de ir para as propriedades para selecionar os novos itens. Utilize o seguinte procedimento para configurar classificações e produtos a sincronizar.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar classificações e produtos a sincronizar  

1.  No **do Configuration Manager** consola, navegue até à **administração** > **configuração do Site** > **Sites**.

2. Selecione o site de administração central ou site primário autónomo.  

3.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.

4.  No separador **Classificações** , especifique as classificações de atualização de software para as quais quer sincronizar atualizações de software.  

    > [!NOTE]  
    >  Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualizações. Durante o processo de sincronização, serão sincronizados os metadados de atualizações de software para as classificações especificadas. O Configuration Manager oferece a capacidade para sincronizar atualizações de software com as seguintes classificações de atualização:  
    >   
    > - **Atualizações críticas**: Especifica uma atualização amplamente lançada para um problema específico que corrige um erro crítico não relacionado com segurança.  
    > - **Atualizações de definições**: Especifica uma atualização para o vírus ou outros ficheiros de definição.  
    > - **Pacotes de funcionalidades**: Especifica as novas funcionalidades de produto que são distribuídas fora de uma versão de produto e que normalmente estão incluídas na próxima versão completa do produto.  
    > - **Atualizações de segurança**: Especifica uma atualização amplamente lançada para um problema específico do produto, relacionadas com a segurança.  
    > - **Pacotes de serviço**: Especifica um conjunto cumulativo de correções que são aplicadas a uma aplicação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.  
    > - **Ferramentas**: Especifica um utilitário ou funcionalidade que ajuda a efetuar uma ou mais tarefas.  
    > - **Update Rollups**: Especifica um conjunto cumulativo de correções que são agrupadas para facilitar a implementação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um rollup de atualizações resolve geralmente uma área específica, tal como segurança ou um componente de produto.  
    > - **Atualizações**: Especifica uma atualização para uma aplicação ou um ficheiro que está atualmente instalado.  
    > - **Atualizar**: Especifica uma atualização para funcionalidades do Windows 10.  
    >   
    >      Os pontos de atualização de software e sites têm de executar um mínimo de WSUS 4.0 com o [correção 3095113](https://support.microsoft.com/kb/3095113) para obter o **atualizar** classificação.  

5.  No separador **Produtos** , especifique os produtos para os quais quer sincronizar atualizações de software e, em seguida, clique em **Fechar**.  

    > [!NOTE]  
    >  Os metadados para cada atualização de software definem os produtos para os quais a atualização é aplicável. Um produto é uma edição específica de um sistema operativo ou aplicação, como o Windows Server 2012. Uma família de produtos é o sistema operativo base ou a aplicação a partir da qual derivam os produtos individuais. Um exemplo de uma família de produtos é o Windows, do qual o Windows Server 2012 é membro. Pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos. Quantos mais produtos selecionar, mais tempo demorará para sincronizar atualizações de software.  
    >   
    >  Quando as atualizações de software serem aplicam a vários produtos e pelo menos um dos produtos foi selecionado para sincronização, todos os produtos aparecerão na consola do Configuration Manager, mesmo se alguns produtos não foram selecionados. Por exemplo, se o Windows Server 2012 é o único sistema operativo que selecionou, e se uma atualização de software se aplicar ao Windows 8 e Windows Server 2012, ambos os produtos serão apresentados na consola do Configuration Manager.  

    > [!IMPORTANT]  
    >  Gestor de configuração armazena uma lista de produtos e famílias de produtos a partir do qual pode escolher quando instalar pela primeira vez o software de ponto de atualização. Produtos e famílias de produtos que são lançadas após o lançamento do Configuration Manager poderão não estar disponíveis para seleção até concluir a sincronização de atualizações de software, que atualiza a lista de produtos disponíveis e famílias de produtos a partir do qual pode escolher.  


## <a name="next-steps"></a>Passos seguintes
Inicie sincronização de atualizações de software para obter as atualizações de software com base nos critérios de novo. Para obter mais detalhes, consulte o artigo [sincronizar atualizações de software](synchronize-software-updates.md).
