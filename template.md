---
title:
- TÍTULO do artigo em 35 carateres ou menos
titleSuffix: Configuration Manager
description: ''
ms.date: mm/dd/yyyy
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid:
- GET ONE FROM guidgenerator.com
author:
- GITHUB USERNAME
ms.author:
- ALIAS
manager:
- ALIAS
ms.openlocfilehash: bb0a23b8870d31136967b1bc594580bcc2cd0cd9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351956"
---
# <a name="metadata-and-markdown-template"></a>Os metadados e o modelo de Markdown

Este modelo docs.ms contém exemplos de sintaxe de markdown, bem como orientações sobre a definição de metadados. Está disponível no diretório de raiz de cada repositório EM piloto (por exemplo, ~/Azure-RMSDocs-pr /template.md) e destina-se a ser lido como um ficheiro de markdown, embora possa consultar a [a versão publicada](https://stage.docs.microsoft.com/en-us/rights-management/template) para ver como os exemplos de markdown são compostos.

Ao criar um ficheiro de markdown, deve copiar o modelo para um novo ficheiro, preencher os metadados conforme especificado abaixo, o cabeçalho H1 acima para o título do artigo e eliminar o conteúdo.


## <a name="metadata"></a>Metadados

O bloco de metadados completo está acima, dividido em campos obrigatórios e opcionais campos; consulte o [cábula de metadados OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) para obter mais detalhes. Algumas notas essenciais:

- **Tem** tem um espaço entre os dois pontos (:) e o valor para um elemento de metadados.
- Se um elemento de metadados opcional não tiver um valor, comente o elemento com um # (não o deixe em branco nem utilize o "ND"); Se estiver a adicionar um valor para um elemento que foi comentado, lembre-se de que remove o #.
- Dois pontos num valor (por exemplo, um título) interromper o parser de metadados. No seu lugar, utilize a codificação HTML de &#58; (por exemplo, "título: O Azure Rights Management&#58; as noções básicas | O Azure RMS").
- **título**: Este título será apresentado nos resultados do motor de pesquisa. O título deve terminar com uma barra vertical (|) seguida do nome do serviço (consulte exemplo acima). O título não precisa (e provavelmente não deve) de ser idêntico ao título do cabeçalho H1. Deve ter cerca de 65 carateres (incluindo | NOME DO SERVIÇO)
- **autor**, **manager**, **revisor**: O campo autor deve conter o **nome de utilizador do Github** do autor, não o alias.  Os campos "Gestor" e "revisor", por outro lado, devem conter aliases. MS. Reviewer Especifica o nome do PM associado ao serviço ou ao artigo.
- **MS. AssetID**: Este é o GUID do artigo a partir de CAPS. Ao criar um novo ficheiro de markdown, obtenha um GUID em [ https://www.guidgenerator.com ](https://www.guidgenerator.com).
- **MS. Prod**, **MS. Service**, **MS. Technology**, **MS. devlang**, **MS. topic**, **MS. tgt_pltfrm** : Os valores possíveis para estes elementos podem ser encontrados [aqui](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## <a name="basic-markdown-and-gfm"></a>Markdown básico e GFM

Todos os markdown básicos e caraterísticos do Github é suportada. Para obter mais informações acerca deste assunto, consulte:

- [Sintaxe de markdown de linha de base](https://daringfireball.net/projects/markdown/syntax)
- [Documentação markdown característico do Github (GFM)](https://guides.github.com/features/mastering-markdown)

## <a name="headings"></a>Cabeçalhos

São exemplos de títulos de primeiro e segundo nível acima.

Não existe **tem** ser apenas um cabeçalho de primeiro nível no tópico, que será apresentado como título na página.  

Cabeçalhos de segundo nível irão gerar o TOC na página que aparece na secção "neste artigo" sob o título na página.

### <a name="third-level-heading"></a>Cabeçalho de terceiro nível
#### <a name="fourth-level-heading"></a>Cabeçalho de quarto nível
##### <a name="fifth-level-heading"></a>Cabeçalho de quinto nível
###### <a name="sixth-level-heading"></a>Cabeçalho de sexto nível

## <a name="text-styling"></a>Estilo de texto

*Italics*

**Bold**

~~Strikethrough~~



## <a name="links"></a>Ligações

Para ligar a um ficheiro de markdown no mesmo repositório, utilize [ligações relativas](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Exemplo: [O que é o Azure Rights Management](./understand-explore/what-is-azure-rights-management.md)

Para ligar a um cabeçalho no mesmo ficheiro de markdown, veja a origem do artigo publicado, localize o id do cabeçalho (por exemplo, `id="blockquote"`e ligue através de # + id (por exemplo, `#blockquote`).

- Exemplo: [Trechos em bloco](#blockquote)

Para ligar a um cabeçalho num ficheiro de markdown no mesmo repositório, utilize relativas + ligações de hashtag da ligação.

- Exemplo: [descrição geral técnica do processo de inscrição](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Para ligar a um ficheiro externo, utilize o URL completo como a ligação.

- Exemplo: [Github](http://www.github.com)

Se aparecer um URL num ficheiro de markdown, será transformado numa ligação clicável.

- Exemplo: http://www.github.com

## <a name="lists"></a>Apresenta uma lista de

### <a name="ordered-lists"></a>Listas ordenadas

1. Isto
1. é
1. um
1. ordenadas
1. List  


#### <a name="ordered-list-with-an-embedded-list"></a>Lista ordenada com uma lista incorporada

1. Aqui
1. é fornecido
1. um
1. incorporados
    1. Menina Isabel
    1. Professor Brandão
1. ordenadas
1. lista


### <a name="unordered-lists"></a>Listas não ordenadas

- Isto
- é
- A
- com marcas
- lista


##### <a name="unordered-list-with-an-embedded-lists"></a>Lista não ordenada com listas incorporadas

- Isto
- com marcas
- lista
    - Senhora Peacock
    - Dr. Pacheco
- contém  
- Outros
    1. Coronel Monteiro
    1. Senhora Ana
- Apresenta uma lista de


## <a name="horizontal-rule"></a>Régua horizontal

---

## <a name="tables"></a>Tabelas

| Tabelas        | São           | Esporádico  |
| ------------- |:-------------:| -----:|
| a col. 3 está      | alinhada à direita | $1600 |
| a col. 2 está      | centra-se      |   $12 |
| a col. 1 é a predefinição | alinhada à esquerda     |    $1 |


## <a name="code"></a>Código

### <a name="codeblock"></a>Bloco de código

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>Código em linha

Este é um exemplo de `in-line code`.

## <a name="blockquotes"></a>Trechos em bloco

> A seca já durava para dez milhões de anos, e o Reinado dos terríveis lagartos há muito havia terminado. Aqui no Equador, no continente que um dia seria possível conhecido como África, a luta pela existência chegara a um novo clímax de ferocidade, e a se sabia quem seria ainda não foi ainda vencedor. Este telefone deserta e árida, apenas os pequenos ou o swift ou os ferozes foi prosperar, ou mesmo hope sobreviver.

## <a name="images"></a>Imagens

### <a name="static-image"></a>Imagem estática

![Este é o texto alternativo](./media/AzRMS_elements.png)

### <a name="linked-image"></a>Imagem ligada

[![texto alternativo para a imagem ligada](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>gif animado

![gif animado](./media/hololens.gif)

## <a name="alerts"></a>Alertas

### <a name="note"></a>Nota

> [!NOTE]
> Este é nota

### <a name="warning"></a>Aviso

> [!WARNING]
> Isto indica um aviso

### <a name="tip"></a>Sugestão

> [!TIP]
> Trata-se de sugestão

### <a name="important"></a>Importante

> [!IMPORTANT]
> Isto é importante

## <a name="videos"></a>Vídeos

### <a name="channel-9"></a>Canal 9

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
- [Barra](/rights-management/scratch.md)

### <a name="step-by-step"></a>Passo a passo

>[!div class="step-by-step"]
[Pre](https://www.example.com)
[seguinte](https://www.example.com)
