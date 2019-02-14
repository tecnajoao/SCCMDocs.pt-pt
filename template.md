---
title:
- TÍTULO do artigo em 35 carateres ou menos
titleSuffix: Configuration Manager
description: ''
ms.date: mm/dd/yyyy
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid:
- PowerShell New-Guid cmdlet
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c586cda33a930478f95f5d2ed1458728c387be21
ms.sourcegitcommit: 66bbdcc5ca18c2a45d13902d5855153c88e56759
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/13/2019
ms.locfileid: "56225383"
---
# <a name="metadata-and-markdown-template"></a>Metadados e o modelo de Markdown

Este modelo docs.ms contém exemplos de sintaxe de markdown, bem como orientações sobre a definição de metadados. Ele está disponível no diretório de raiz de cada repositório EM piloto (por exemplo, ~/Azure-RMSDocs-pr/Template.MD) e se destina a ser lido como um ficheiro de markdown, embora possa consultar a [a versão publicada](https://stage.docs.microsoft.com/en-us/rights-management/template) para ver como os exemplos de markdown são compostos.

Ao criar um ficheiro de markdown, deve copiar o modelo para um novo ficheiro, preencher os metadados conforme especificado abaixo, o cabeçalho H1 acima para o título do artigo e eliminar o conteúdo.


## <a name="metadata"></a>Metadados

O bloco de metadados completo está acima, dividido em campos obrigatórios e opcionais campos; consulte a [cábula de metadados OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) para obter mais detalhes. Algumas notas essenciais:

- **Tem** tem um espaço entre os dois pontos (:) e o valor para um elemento de metadados.
- Se um elemento de metadados opcional não tiver um valor, comente o elemento com um # (não o deixe em branco nem utilize o "ND"); Se estiver a adicionar um valor para um elemento que foi comentado, certifique-se de que remove o #.
- Dois pontos num valor (por exemplo, um título) quebram o parser de metadados. Em vez disso, utilize a codificação HTML de &#58; (por exemplo, "título: O Azure Rights Management&#58; Noções básicas | O Azure RMS").
- **title**: Este título será apresentado nos resultados do motor de pesquisa. O título deve terminar com uma barra vertical (|) seguida do nome do serviço (por exemplo, consulte acima). O título não precisa (e provavelmente não devem) ser idêntico ao título do cabeçalho H1. Deve ter cerca de 65 carateres (incluindo | NOME DO SERVIÇO)
- **author**, **manager**, **reviewer**: O campo autor deve conter a **nome de utilizador do Github** do autor, não o alias.  Os campos "Gestor" e "revisor", por outro lado, devem conter aliases. MS. Reviewer Especifica o nome do PM associado ao serviço ou ao artigo.
- **ms.assetid**: Este é o GUID do artigo a partir de CAPS. Ao criar um novo ficheiro de markdown, obtenha um GUID em [ https://www.guidgenerator.com ](https://www.guidgenerator.com).
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: Valores possíveis para esses elementos podem ser encontrados [aqui](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## <a name="basic-markdown-and-gfm"></a>Markdown básico e GFM

Todos os markdown básicos e caraterísticos do Github é suportada. Para obter mais informações sobre elas, consulte:

- [Sintaxe de markdown de linha de base](https://daringfireball.net/projects/markdown/syntax)
- [Documentação markdown com caraterísticas do Github (GFM)](https://guides.github.com/features/mastering-markdown)

## <a name="headings"></a>Cabeçalhos

São exemplos de títulos de primeiro e segundo nível acima.

Existem **tem** ser apenas um cabeçalho de primeiro nível no tópico, que será apresentado como título na página.  

Cabeçalhos de segundo nível irão gerar o índice na página que aparece na secção "de entrada neste artigo" sob o título na página.

### <a name="third-level-heading"></a>Cabeçalho de terceiro nível
#### <a name="fourth-level-heading"></a>Cabeçalho de quarto nível
##### <a name="fifth-level-heading"></a>Cabeçalho de quinto nível
###### <a name="sixth-level-heading"></a>Cabeçalho de sexto nível

## <a name="text-styling"></a>Estilos de texto

*Itálico*

**Negrito**

~~Rasurado~~



## <a name="links"></a>Links

Para ligar a um ficheiro de markdown no mesmo repositório, utilize [ligações relativas](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Exemplo: [O que é o Azure Rights Management](./understand-explore/what-is-azure-rights-management.md)

Para ligar a um cabeçalho no mesmo ficheiro de markdown, veja a origem do artigo publicado, localize o id do cabeçalho (por exemplo, `id="blockquote"`e ligue através de # + id (por exemplo, `#blockquote`).

- Exemplo: [Trechos em bloco](#blockquote)

Para ligar a um cabeçalho num ficheiro de markdown no mesmo repositório, utilize ligações relativas + ligações hashtag de ligação.

- Exemplo: [descrição geral técnica do processo de inscrição](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Para ligar a um arquivo externo, utilize o URL completo como a ligação.

- Exemplo: [Github](http://www.github.com)

Se aparecer um URL num ficheiro de markdown, será transformado numa ligação clicável.

- Exemplo: http://www.github.com

## <a name="lists"></a>Apresenta uma lista

### <a name="ordered-lists"></a>Listas ordenadas

1. Isto
1. Is
1. Um
1. Ordenado
1. List  


#### <a name="ordered-list-with-an-embedded-list"></a>Lista ordenada com uma lista incorporada

1. Aqui
1. vem
1. an
1. Incorporado
    1. Menina Isabel
    1. Professor Brandão
1. Ordenado
1. list


### <a name="unordered-lists"></a>Listas não ordenadas

- Isto
- is
- a
- com marcadores
- list


##### <a name="unordered-list-with-an-embedded-lists"></a>Lista não ordenada com listas incorporadas

- Isto
- com marcadores
- list
    - Sra. corte-real
    - Dr. Pacheco
- Contém  
- Outros
    1. Coronel Monteiro
    1. Senhora Ana
- Apresenta uma lista


## <a name="horizontal-rule"></a>Régua horizontal

---

## <a name="tables"></a>Tabelas

| Tabelas        | São           | Acesso esporádico  |
| ------------- |:-------------:| -----:|
| a col. 3 está      | alinhado à direita | $1600 |
| a col. 2 está      | centralizado      |   $12 |
| a col. 1 é a predefinição | alinhados à esquerda     |    $1 |


## <a name="code"></a>Código

### <a name="codeblock"></a>Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>Na linha de código

Este é um exemplo de `in-line code`.

## <a name="blockquotes"></a>Trechos em bloco

> A seca durava há dez milhões de anos e o Reinado dos terríveis lagartos. há muito havia muito tempo terminou. Aqui no Equador, no continente que um dia seria ser conhecido como África, a batalha existência tinha atingido um novo clímax de ferocidade, e o victor ainda não tinha sido vistos. Esta situação modesta e árida, apenas as pequenas ou de swift ou os poderiam prosperem ou sequer esperar sobreviver.

## <a name="images"></a>Imagens

### <a name="static-image"></a>Imagem estática

![Este é o texto alternativo](./media/AzRMS_elements.png)

### <a name="linked-image"></a>Imagem ligada

[![texto alternativo para a imagem ligada](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>Gif animado

![gif animado](./media/hololens.gif)

## <a name="alerts"></a>Alertas

### <a name="note"></a>Nota

> [!NOTE]
> Isto indica uma nota

### <a name="warning"></a>Aviso

> [!WARNING]
> Isto indica um aviso

### <a name="tip"></a>Sugestão

> [!TIP]
> Isto é sugestão

### <a name="important"></a>Importante

> [!IMPORTANT]
> Isto é importante

## <a name="videos"></a>Vídeos

### <a name="channel-9"></a>Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### <a name="youtube"></a>YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## <a name="docsms-extentions"></a>extensões do Docs.MS

### <a name="button"></a>Botão

> [!div class="button"]
[ligações de botão](/rights-management)

### <a name="selector"></a>Seletor

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### <a name="step-by-step"></a>Passo a passo

>[!div class="step-by-step"]
[Pré](https://www.example.com)
[seguinte](https://www.example.com)
