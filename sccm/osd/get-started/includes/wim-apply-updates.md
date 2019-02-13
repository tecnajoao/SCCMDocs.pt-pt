---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 11/27/2018
ms.openlocfilehash: f6e46f8b0bf985eae87cd5157f8a82af5fa0b849
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142583"
---
##  <a name="BKMK_OSImagesApplyUpdates"></a> Aplicar atualizações de software a uma imagem  

> [!Note]  
> Esta secção aplica-se a ambos **imagens do sistema operacional** e **pacotes de atualização de SO**. Utiliza o termo geral "imagem" para referenciar o ficheiro de imagem do Windows (WIM). Esses objetos têm um WIM, que contém ficheiros de instalação do Windows. Atualizações de software são aplicáveis a esses arquivos em ambos os objetos. O comportamento desse processo é o mesmo entre os dois objetos.  

Todos os meses existem novas atualizações de software aplicáveis para a imagem. Antes de poder aplicar as atualizações de software ao mesmo, tem os seguintes pré-requisitos: 

- Infraestrutura de atualizações de software  
- Atualizações de software sincronizadas com êxito  
- Transferir as atualizações de software para a biblioteca de conteúdos no servidor do site  

Para obter mais informações, consulte [implementar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).  

Aplica atualizações de software aplicáveis a uma imagem numa agenda especificada. Este processo é por vezes, denominado *em serviços offline*. Esta agenda, Configuration Manager aplica-se as atualizações de software selecionadas para a imagem. Ele, em seguida, também pode redistribuir a imagem atualizada para pontos de distribuição. 

A base de dados armazena informações sobre a imagem, incluindo as atualizações de software que foram aplicadas no momento da importação. Atualizações de software que se aplicam à imagem de uma vez que esta foi inicialmente adicionada também são armazenadas na base de dados do site. Quando inicia o Assistente para aplicar atualizações de software, ele obtém a lista de atualizações de software aplicáveis que o site ainda não tenha aplicadas à imagem. Gestor de configuração copia as atualizações de software que selecionar da biblioteca de conteúdos no servidor do site. Em seguida, aplica as atualizações de software à imagem.  


### <a name="servicing-process"></a>Processo de manutenção  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, selecione **imagens do sistema operativo** ou  **Pacotes de atualização do sistema operativo**.  

2.  Selecione o objeto ao qual pretende aplicar atualizações de software.  

3.  No Friso, selecione **agendar atualizações** para iniciar o assistente.  

4.  Sobre o **escolher as atualizações** página, selecione as atualizações de software para aplicar à imagem. Pode demorar algum tempo para a lista de atualizações seja apresentado no assistente. Utilize o **filtro** para pesquisar cadeias de caracteres nos metadados. Utilize o **arquitetura do sistema** na lista pendente para filtrar os **X86**, **X64**, ou **todos os**. Pode selecionar uma, várias ou todas as atualizações na lista. Quando tiver terminado de selecionar atualizações, selecione **seguinte**.  

5.  Na página **Definir Agendamento** , especifique as seguintes definições e clique em **Seguinte**.  

    a.  **Agenda**: Especifique a agenda para quando o site aplica as atualizações de software à imagem.  

    b.  **Continuar com o erro**:  Selecione esta opção para continuar a aplicar atualizações de software à imagem, mesmo se ocorrer um erro.  

    c.  **Atualizar pontos de distribuição com a imagem**: Selecione esta opção para atualizar a imagem em pontos de distribuição depois do site aplica-se as atualizações de software.  

6.  Conclua o Assistente de atualizações de agenda.  

> [!NOTE]  
>  Para minimizar o tamanho da carga, a manutenção de pacotes de atualização do SO e imagens do sistema operacional remove a versão mais antiga.  


### <a name="servicing-operations"></a>As operações de serviço

Na consola do Configuration Manager, em qualquer um de **imagens do sistema operacional** ou **pacotes de atualização de SO** nó, adicione as seguintes colunas para a vista:
- **Data de atualizações agendada**: Esta propriedade mostra a agenda seguinte que definir.  
- **Agendado o estado das atualizações**: Esta propriedade mostra o estado. Por exemplo, **Successful** ou **processo**.  

Selecione um objeto de imagem específica e, em seguida, mude para o **estado de atualização** separador no painel de detalhes. Este separador mostra a lista de atualizações na imagem. 

Selecione um objeto de imagem específica e selecione **propriedades** na faixa de opções. O **atualizações instaladas** separador mostra a lista de atualizações na imagem. O **manutenção** guia é uma vista só de leitura da agenda de manutenção atual e as atualizações que tenha programado para aplicar. 

Quando o estado é **processo**, pode selecionar **Cancelar atualizações agendadas** da faixa de opções. Esta ação cancela o processo de serviço Active Directory. 

Para resolver este processo, veja a **OfflineServicingMgr.log** e **DISM** ficheiros no servidor do site. Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files).


### <a name="bkmk_servicing-drive"></a> Especifique a unidade para a manutenção da imagem de SO offline  
<!--1358924-->

A partir da versão 1810, especifique a unidade que o Configuration Manager utiliza durante a manutenção offline de imagens do sistema operacional. Este processo pode consumir uma grande quantidade de espaço em disco com ficheiros temporários. Esta opção dá-lhe flexibilidade para selecionar a unidade a utilizar. 

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. No Friso, clique em **configurar componentes do Site** e selecione **implementação do sistema operativo**.  

2. Sobre o **fornecimento Offline** separador, especifique a opção para **uma unidade local a ser utilizado pelo fornecimento offline de imagens**.  

Por predefinição, esta definição é **automática**. Com este valor, o Configuration Manager seleciona a unidade onde está instalado. 

Se selecionar uma unidade que não existe no servidor do site, o Configuration Manager tem o mesmo comportamento como se selecionou **automática**. 

Durante a manutenção offline, o Configuration Manager armazena ficheiros temporários na pasta, `<drive>:\ConfigMgr_OfflineImageServicing`. Ele também monta a imagem do SO nesta pasta. 


