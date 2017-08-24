---
title: "Criar itens de configuração para o Configuration Manager do cliente gerido Macs - | Microsoft Docs"
description: "Utilize o item de configuração do Mac OS X do System Center Configuration Manager para gerir as definições para dispositivos Mac OS X."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 541e5ad629a9e2ed9c353dff150f9b86b9d12b7d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para dispositivos Mac OS X geridos com o cliente System Center Configuration Manager
Utilizar o System Center Configuration Manager**Mac OS X (personalizado)** item de configuração para gerir as definições para dispositivos Mac OS X que são geridos pelo cliente do Configuration Manager.  
  
 O sistema operativo Mac OS X utiliza ficheiros de lista de propriedades (ou plist) para armazenar as definições das aplicações. Utilize as definições de compatibilidade para avaliar e corrigir as definições num ficheiro de lista de propriedades. Também pode gerir as definições de Mac OS X ao escrever um Script de Shell que devolva um valor que pode avaliar e corrigir para fins de compatibilidade.  
  
### <a name="to-create-a-custom-mac-os-x-configuration-item"></a>Para criar um item de configuração do Mac OS X personalizado  
  
1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade**.  
  
2.  Na área de trabalho **Ativos e Conformidade** , expanda **Definições de Conformidade**e, em seguida, clique em **Itens de Configuração**.  
  
3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Mac OS X (personalizado)**.  
  
6.  Clique em **categorias** se criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  
  
7.  Na página **Plataformas Suportadas** do assistente, selecione as versões do Mac OS X específicas que irão avaliar o item de configuração.  
  
8.  Na página **Definições** do assistente, terá de adicionar novas definições cuja compatibilidade em computadores Mac será avaliada. Clique em **Nova** para abrir a caixa de diálogo **Criar Definição**.  
  
9. Na caixa de diálogo **Criar Definição**, introduza um nome único e uma descrição para a definição.  
  
10. Escolha o **Tipo de Definição** que pretende e, em seguida, escreva as informações necessárias, conforme apresentado na seguinte tabela:  
  
    -   **Preferências do Mac OS X** -  
  
        -   **ID da Aplicação** – especifique o ID da aplicação do ficheiro de lista de propriedades a partir do qual pretende avaliar a compatibilidade de uma chave.  
  
             Por exemplo, se pretender editar as definições do browser Safari, poderá utilizar **com.apple.Safari.plist**.  
  
        -   **Chave** – especifique o nome da chave cuja compatibilidade quer avaliar nos computadores Mac. Utilize a sintaxe */<dictionary\>/<keyname\>*.  
  
            > [!IMPORTANT]  
            >  O nome da chave é sensível a maiúsculas e minúsculas e não será avaliado caso seja diferente do nome da chave no computador Mac. Além disso, não é possível editar o nome da chave depois de o ter especificado. Se precisar de editar o nome da chave, elimine a definição e, em seguida, recrie-a.  
  
    -   **Script** -  
  
        -   **Script de Deteção** – clique em **Adicionar Script** e, em seguida, introduza um script de shell para avaliar a compatibilidade das definições no computador Mac. Utilize o **eco** comando no script de shell para devolver valores para o Configuration Manager para compatibilidade. O Configuration Manager utiliza os resultados devolvidos no **STDOUT** para avaliar a compatibilidade.  
  
            > [!IMPORTANT]  
            >  Não inclua o comando **reiniciar** no script de deteção. Uma vez que o script de deteção é executado sempre que o cliente é reiniciado, isto fará com que o computador Mac reinicie continuamente.  
  
        -   **Script de remediação (opcional)** -opcionalmente, clique em **Adicionar Script** e, em seguida, introduza um script de shell utilizado para corrigir as definições não compatíveis encontradas nos computadores cliente Mac.  
  
            > [!IMPORTANT]  
            >  Para garantir que não introduz carateres de formatação que o computador Mac não consegue interpretar, em vez de copiar e colar, escreva o script.  
  
11. Escolha o **Tipo de dados** que é o formato no qual a condição devolve os dados antes de ser utilizada para avaliar a definição.  
  
    > [!NOTE]  
    >  O tipo de dados **Vírgula flutuante** suporta apenas três dígitos depois da casa decimal.  
    >   
    >  O Configuration Manager não suporta a utilização de **booleano** tipo de dados para definições de script de item de configuração de Mac. Em alternativa, defina o tipo de dados como **Número inteiro** e certifique-se de que o script devolve um valor inteiro.  
  
12. Clique em **OK** para guardar a definição, feche a caixa de diálogo **Criar Definição** e, em seguida, continue a adicionar as definições que forem necessárias.  
  
13. Na página **Regras de Compatibilidade** do assistente, vai especificar as condições que definem a compatibilidade de um item de configuração. Antes de poder ser avaliada a compatibilidade de uma definição, esta tem de ter, pelo menos, uma regra de compatibilidade. Clique em **Nova** para adicionar uma nova regra.  
  
14. Na caixa de diálogo **Criar Regra**, forneça as seguintes informações:  
  
    -   **Nome:** Introduza um nome para a regra de compatibilidade.  
  
    -   **Descrição:** Introduza uma descrição para a regra de compatibilidade.  
  
    -   **Definição selecionada:** Clique em **procurar** para abrir o **selecionar definição** caixa de diálogo. Selecione a definição na qual pretende definir uma regra ou clique em **Nova Definição**. Quando terminar, clique em **Selecionar**.  
  
        > [!TIP]  
        >  Também pode clicar em **Propriedades** para ver informações sobre a definição atualmente selecionada.  
  
    -   **Tipo de regra:** Selecione o tipo de regra de compatibilidade que pretende utilizar:  
  
        -   **Valor:** Crie uma regra que compara o valor devolvido pelo item de configuração em relação a um valor que especificar.  
  
        -   **Existencial** - crie uma regra que avalie a definição dependendo de existir num dispositivo.  
  
    -   Num tipo de regra de **Valor**, especifique as seguintes informações:  
  
        -   A definição deve estar em conformidade com a seguinte regra – Selecione um operador e um valor que é avaliado quanto à compatibilidade com a definição selecionada. Pode utilizar os seguintes operadores:  
  
            -   **Igual a**  
  
            -   **Não é igual a**  
  
            -   **Maior que**  
  
            -   **Inferior a**  
  
            -   **Entre**  
  
            -   **Maior ou igual a**  
  
            -   **Menor ou igual a**  
  
            -   **Um de** - na caixa de texto, especifique uma entrada em cada linha.  
  
            -   **Nenhum de** - na caixa de texto, especifique uma entrada em cada linha.  
  
        -   **Remediar regras incompatíveis quando suportado** – selecione esta opção se pretender que o Configuration Manager retifique automaticamente as regras incompatíveis.  
  
            > [!IMPORTANT]  
            >  Só pode remediar regras incompatíveis quando o operador de regra estiver definido como **É igual a**.  
  
        -   **Comunicar incompatibilidade se não for encontrada a instância desta definição** – o item de configuração comunica a incompatibilidade se esta definição não for encontrada no computador Mac.  
  
    -   **Gravidade de incompatibilidade para relatórios** - especifica o nível de gravidade reportado se esta regra de compatibilidade falhar. Os níveis de gravidade disponíveis são os seguintes:  
  
        -   **Nenhum** -computadores que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  
  
        -   **Informações** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.  
  
        -   **Aviso** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.  
  
        -   **Crítico** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager.  
  
        -   **Crítico com evento** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager. Este nível de gravidade também é registado pelo computador cliente Mac.  
  
    -   Para um tipo de regra **Existencial**, especifique as seguintes informações:  
  
        -   Escolha um dos seguintes:  
  
            -   **A definição deve existir nos dispositivos cliente**  
  
            -   **A definição não deve existir nos dispositivos cliente**  
  
        -   **Gravidade de incompatibilidade para relatórios:** Especifique o nível de gravidade reportado se esta regra de compatibilidade falhar. Os níveis de gravidade disponíveis são os seguintes:  
  
            -   **Nenhum** -computadores que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  
  
            -   **Informações** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.  
  
            -   **Aviso** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.  
  
            -   **Crítico** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager.  
  
            -   **Crítico com evento** -os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager. Este nível de gravidade também é registado pelo computador cliente Mac.  
  
        > [!NOTE]  
        >  As opções apresentadas podem variar consoante o tipo de definição para o qual está a configurar uma regra.  
  
    -   Clique em **OK** para fechar a caixa de diálogo **Criar Regra**.  
  
15. Na página **Resumo**, confirme as definições do novo item de configuração e, em seguida, conclua o assistente.  
  
 O novo item de configuração é apresentado no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade**.  
  
 Se pretender agora adicionar este item de configuração a uma linha de base de configuração, veja [Como criar linhas de base de configuração no System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Itens de configuração para dispositivos geridos com o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
