---
title: A ferramenta de limpeza da biblioteca de conteúdos
titleSuffix: Configuration Manager
description: Utilize a ferramenta de limpeza da biblioteca de conteúdos para remover o conteúdo órfão já não está associado a uma implementação do System Center Configuration Manager.
ms.date: 4/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3a091a526a385fadf0353073048d33ae704cd76
ms.sourcegitcommit: f9b11bb0942cd3d03d90005b1681e9a14dc052a1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/24/2018
ms.locfileid: "39229376"
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>A ferramenta de limpeza da biblioteca de conteúdos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 A partir da versão 1702, pode usar uma ferramenta de linha de comandos (**ContentLibraryCleanup.exe**) remover o conteúdo que é mais longo para não associado a nenhum pacote ou aplicação a partir de um ponto de distribuição (órfão conteúdo). Essa ferramenta denomina-se a ferramenta de limpeza da biblioteca de conteúdos e substitui as versões anteriores das ferramentas similares lançadas nos últimos produtos do Configuration Manager.  

A ferramenta só afeta o conteúdo no ponto de distribuição que especifica quando executar a ferramenta. A ferramenta não é possível remover o conteúdo da biblioteca de conteúdos no servidor do site.

Pode encontrar **ContentLibraryCleanup.exe** no \*%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* pasta no servidor do site num site de administração central ou site primário.

## <a name="requirements"></a>Requisitos  
 A ferramenta só pode executar em relação a um único ponto de distribuição de cada vez.  
 - Pode ser executada diretamente no computador que aloja o ponto de distribuição que pretende limpar, ou remotamente a partir de outro servidor.
 - A conta de utilizador que executa a ferramenta tem de ter permissões de administração baseada em funções direto que sejam iguais a um administrador total na hierarquia do Configuration Manager. A ferramenta não funciona quando a conta recebe essas permissões como membro de um grupo de segurança do Windows que tem as permissões de administrador completo.

## <a name="modes-of-operation"></a>Modos de funcionamento
Pode executar a ferramenta nos seguintes dois modos. Recomendamos que execute a ferramenta no *hipóteses* modo para poder rever os resultados antes de executar a ferramenta *eliminar modo*:
  1.    **Modo de hipóteses**:   
      Se não especificar a **/eliminar** comutador, a ferramenta é executada no modo de hipóteses e identifica os conteúdos que serão eliminados do ponto de distribuição.
   - Ao serem executados neste modo a ferramenta não elimina quaisquer dados.
   - Informações sobre o conteúdo que será eliminado são escritas para o ficheiro de registo de ferramentas, e não for solicitado a confirmar a cada eliminação potencial.  
      </br>   

  2. **Eliminar modo**:   
    Quando executa a ferramenta com o **/eliminar** comutador, a ferramenta é executada no modo de eliminação.

     - Ao serem executados neste modo, o conteúdo órfão que se encontra no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.
     -  Antes de excluir cada arquivo, tem de confirmar que o ficheiro deve ser eliminado.  Pode selecionar, **Y** para Sim, **N** para não, ou **Sim para todos os** para ignorar a outros prompts e eliminar conteúdo órfão tudo.  
     </br>

Quando a ferramenta é executada no modo de ambos, este cria automaticamente um registo com um nome que inclui o modo da que ferramenta é executada, o nome do ponto de distribuição e a data e hora da operação. O ficheiro de registo abre-se automaticamente quando a ferramenta é concluída.

Por predefinição, o ficheiro de registo é escrito para a pasta temporária da conta de utilizador que executa a ferramenta, no computador onde a ferramenta é executada. Pode utilizar o **/log** comutador para redirecionar o ficheiro de registo para outro local, incluindo um compartilhamento de rede.


## <a name="run-the-tool"></a>Execute a ferramenta
Para executar a ferramenta:
1. Abra uma linha de comandos administrativa para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, introduza uma linha de comando que inclui as opções de linha de comandos necessários e opcionais comutadores que pretende utilizar.

**Problema conhecido** quando a ferramenta é executada, pode ser devolvido um erro semelhante ao seguinte, quando nenhum pacote ou implementação falhou ou está em curso:
-  *System.InvalidOperationException: Nesta biblioteca de conteúdos não é possível limpar neste momento porque o pacote <packageID> não está totalmente instalado.*

**Solução:** Nenhuma. A ferramenta de forma fiável não consegue identificar arquivos órfãos quando o conteúdo está em curso ou falhou a implementação. Por conseguinte, a ferramenta não permitirá que para limpar o conteúdo até que esse problema foi resolvido.

### <a name="command-line-switches"></a>Opções de linha de comandos  
Os seguintes parâmetros de linha de comandos podem ser utilizados por qualquer ordem.   

|Parâmetro|Detalhes|
|---------|-------|
|**/delete**  |**Opcional** </br> Use esta opção quando pretender eliminar o conteúdo do ponto de distribuição. É pedido antes do conteúdo é eliminado. </br></br> Quando este comutador não for utilizado, a ferramenta regista resultados sobre o conteúdo que será eliminado, mas não elimina o conteúdo do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Este comutador executa a ferramenta num modo silencioso, que suprime todas as instruções (como as instruções para eliminar conteúdo) e não abre automaticamente o ficheiro de registo. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição >**  | **Necessário** </br> Especifique o nome de domínio completamente qualificado (FQDN) do ponto de distribuição que pretende limpar. </br></br> Exemplo:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/PS &lt;site primário de FQDN >**       | **Opcional** quando limpar o conteúdo de um ponto de distribuição num site primário.</br>**Necessário** quando limpar o conteúdo de um ponto de distribuição num site secundário. </br></br>A ferramenta se conectar ao site primário principal para executar consultas no SMS_Provider. Estas permitem consultas a ferramenta de determinar o conteúdo que deve estar no ponto de distribuição, para que possa identificar o conteúdo que é órfã e pode ser removido. Esta ligação para o site primário principal deve ser tomada para pontos de distribuição num site secundário porque os detalhes necessários não estão disponíveis diretamente a partir do site secundário.</br></br> Especifique o FQDN do site primário que pertence o ponto de distribuição ou do principal primário principal, quando o ponto de distribuição estiver num site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site primário >**  | **Opcional** quando limpar o conteúdo de um ponto de distribuição num site primário.</br>**Necessário** quando limpar o conteúdo de um ponto de distribuição num site secundário. </br></br> Especifique o código do site do site primário que pertence o ponto de distribuição ou de site primário principal, quando o ponto de distribuição estiver num site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Opcional** </br> Especifique a localização onde a ferramenta grava o ficheiro de registo. Isso pode ser uma unidade local ou numa rede de partilhar.</br></br> Quando este comutador não for utilizado, o ficheiro de registo é colocado na pasta temp do utilizador, no computador onde a ferramenta é executada.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de compartilhamento de rede: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\ &lt;partilhar >\&lt; pasta >***|
