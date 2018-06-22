---
title: 'Sincronizar atualizações com nenhuma ligação à Internet '
titleSuffix: Configuration Manager
description: Execute a sincronização de atualizações de software no ponto de atualização de software de nível superior estiver desligado da Internet.
author: aczechowski
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: da6204a78ce45c72d2b8d5586d02c8692405f295
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350430"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Sincronizar atualizações de software a partir de um ponto de atualização de software desligado  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Quando o ponto de atualização de software no site de nível superior está desligado da Internet, terá de utilizar as funções de exportação e importação da ferramenta WSUSUtil para sincronizar os metadados de atualizações de software. Pode escolher um servidor WSUS existente não na hierarquia do Configuration Manager como origem de sincronização. Este tópico fornece informações sobre como utilizar a exportação e importação de funções da ferramenta WSUSUtil.  

 Para exportar e importar metadados de atualizações de software, terá de exportar metadados de atualizações de software a partir da base de dados do WSUS num servidor de exportação especificado e, em seguida, copiar os ficheiros de termos de licenciamento armazenados a nível local para o ponto de atualização de software desligado e, em seguida, importar os metadados de atualizações de software para a base de dados do WSUS no ponto de atualização de software desligado.  

 Utilize a tabela seguinte para identificar o servidor de exportação para o qual pretende exportar os metadados de atualizações de software.  

|Ponto de atualização de software|Origem das atualizações a montante para pontos de atualização de software ligados|Servidor de exportação para um ponto de atualização de software desligado|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Site de administração central|Microsoft Update (Internet)<br /><br /> Servidor WSUS existente|Escolha um servidor WSUS que está sincronizado com o Microsoft Update utilizando as classificações de atualizações de software, produtos e idiomas de que necessita no seu ambiente do Configuration Manager.|  
|Site primário autónomo|Microsoft Update (Internet)<br /><br /> Servidor WSUS existente|Escolha um servidor WSUS que está sincronizado com o Microsoft Update utilizando as classificações de atualizações de software, produtos e idiomas de que necessita no seu ambiente do Configuration Manager.|  

 Antes de iniciar o processo de exportação, verifique se a sincronização de atualizações de software está concluída no servidor de exportação selecionado para garantir a sincronização dos metadados de atualizações de software mais recentes. Para verificar que a sincronização de atualizações do software foi concluída com êxito, utilize o seguinte procedimento.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Para verificar se a sincronização de atualizações do software foi concluída com êxito no servidor de exportação  

1.  Abra a consola de Administração do WSUS e ligue à base de dados do WSUS no servidor de exportação.  

2.  Na consola de Administração do WSUS, clique em **Sincronizações**. Uma lista das tentativas de sincronização de atualizações do software é apresentada no painel de resultados.  

3.  No painel de resultados, encontre a mais recente tentativa de sincronização de atualizações de software e verifique que foi concluída com êxito.  

> [!IMPORTANT]  
>  A ferramenta WSUSUtil tem de ser executada localmente no servidor de exportação para exportar os metadados de atualizações de software e tem também de ser executada no ponto de atualização de software desligado para importar os metadados de atualizações de software. Além disso, o utilizador que executa a ferramenta WSUSUtil tem de ser membro do grupo de Administradores local em cada servidor.  

## <a name="export-process-for-software-updates"></a>Processo de exportação para atualizações de software  
 O processo de exportação para atualizações de software consiste em dois passos principais: copiar os ficheiros de termos de licenciamento armazenados a nível local para o ponto de atualização de software desligado e exportar metadados de atualização de software a partir da base de dados WSUS no servidor de exportação.  

 Utilize o seguinte procedimento para copiar os metadados de termos de licenciamento locais para o ponto de atualização de software desligado.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Para copiar ficheiros locais do servidor de exportação para o servidor de ponto de atualização de software desligado  

1.  No servidor de exportação, navegue para a pasta onde as atualizações de software e os termos de licenciamento para atualizações de software estão armazenados. Por predefinição, o servidor WSUS armazena os ficheiros em <*WSUSInstallationDrive*>\WSUS\WSUSContent\\, onde *WSUSInstallationDrive* é a unidade na qual o WSUS está instalado.  

2.  Copie todos os ficheiros e pastas a partir desta localização para a pasta WSUSContent no servidor de ponto de atualização de software desligado.  

 Utilize o seguinte procedimento para exportar os metadados de atualizações de software da base de dados do WSUS no servidor de exportação.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Para exportar metadados de atualizações de software a partir da base de dados do WSUS no servidor de exportação  

1.  Na linha de comandos no servidor de exportação, aceda à pasta que contém o ficheiro WSUSutil.exe. Por predefinição, a ferramenta está localizada em %*ProgramFiles*%\Update Services\Tools. Por exemplo, se a ferramenta estiver localizada na localização predefinida, escreva **cd %ProgramFiles%\Update Services\Tools**.  

2.  Escreva o seguinte para exportar os metadados de atualizações de software para um ficheiro de pacote:  

     **wsusutil.exe export**  *packagename*  *logfile*  

     Por exemplo:  

     **wsusutil.exe export export.cab export.log**  

     O formato pode ser resumido da seguinte forma: WSUSutil.exe é seguido pela opção de exportação, o nome do ficheiro. cab de exportação criado durante a operação de exportação e o nome de um ficheiro de registo. WSUSutil.exe exporta os metadados do servidor de exportação e cria um ficheiro de registo da operação.  

    > [!NOTE]  
    >  O pacote (ficheiro. cab) e o nome do ficheiro de registo devem ser exclusivos na pasta atual.  

3.  Mova o pacote de exportação para a pasta que contém WSUSutil.exe no servidor WSUS de importação.  

    > [!NOTE]  
    >  Se mover o pacote para esta pasta, a experiência de importação pode ser mais fácil. Pode mover o pacote para qualquer localização que seja acessível ao servidor de importação e, em seguida, especifique a localização quando executar o WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Importar metadados de atualizações de software  
 Utilize o seguinte procedimento para importar os metadados de atualizações de software do servidor de exportação para o ponto de atualização de software desligado.  

> [!IMPORTANT]  
>  Nunca importe quaisquer dados exportados de uma fonte que não seja fidedigna. Se importar conteúdo de uma fonte que não seja fidedigna, tal poderá comprometer a segurança do servidor WSUS.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Para importar metadados para a base de dados do servidor de importação  

1.  Na linha de comandos no servidor WSUS de importação, aceda à pasta que contém o ficheiro WSUSutil.exe. Por predefinição, a ferramenta está localizada em %*ProgramFiles*%\Update Services\Tools.  

2.  Escreva o seguinte:  

     **wsusutil.exe import**  *packagename*  *logfile*  

     Por exemplo:  

     **wsusutil.exe import export.cab import.log**  

     O formato pode ser resumido da seguinte forma: WSUSutil.exe é seguido pelo comando de importação, o nome do ficheiro de pacote (. cab) que é criado durante a operação de exportação, o caminho para o ficheiro de pacote se faz parte de uma pasta diferente e o nome de um ficheiro de registo. WSUSutil.exe importa os metadados do servidor de exportação e cria um ficheiro de registo da operação.  

## <a name="next-steps"></a>Passos seguintes
Depois de sincronizar as atualizações de software pela primeira vez ou depois de existirem novas classificações ou produtos disponíveis, tem [configurar novas classificações e produtos](configure-classifications-and-products.md) para sincronizar atualizações de software com os critérios de novo.

Depois das atualizações de software syncrhonize com os critérios que precisa, [gerir as definições das atualizações de software](manage-settings-for-software-updates.md).  
