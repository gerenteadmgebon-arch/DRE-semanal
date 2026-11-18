# DRE compartilhado — ativação pendente

Esta versão foi preparada e testada; não foi publicada no ambiente de produção.

## Comportamento

- Editor tem as mesmas permissões funcionais do administrador, inclusive gestão de usuários. Leitor somente consulta. O proprietário fixo não pode ser bloqueado.
- E-mails existentes sem perfil explícito passam a ser leitores. A promoção para Editor deve ser feita no cadastro de usuários.
- Um rascunho compartilhado em `gebonDreDrafts/shared_completo`, diários compartilhados por empresa e competência, e histórico comum. UID/e-mail são autoria, não separação dos dados.
- O último rascunho legado é carregado quando ainda não existe rascunho compartilhado. Diários legados são aproveitados na primeira gravação compartilhada; arquivos antigos ficam preservados e sem novas gravações.
- Transações com revisão bloqueiam sobrescrita concorrente. Alterações externas chegam em tempo real; se há edição local pendente, a interface pede recarregamento.
- Visão geral usa data inicial/final. Meses inteiros usam o fechamento; partes do mês usam lançamentos diários. Ajustes mensais sem data não são distribuídos artificialmente. Taxa manual mensal não é aplicada automaticamente a um recorte diário com base financeira não nula; nesse caso o sistema orienta usar CDI automático.
- Excel: duas casas em valores, zeros e percentuais, inclusive Dias salvos; taxas são exportadas como porcentagens numéricas.
- Formulário rápido compacto; menus Importar planilha, Baixar modelo Excel e Relatórios e exportação removidos.

## Validação

21 verificações no emulador Firestore, incluindo gravação bruta recusada para leitor, edição comum, atualização em tempo real, conflito, migração legada, autorização do Editor e rebaixamento de perfil. Testes de intervalo, saldos, comparativos, Excel e 348 valores do modelo original passaram. Interface de Editor e Leitor foi conferida com dados fictícios.

## Ordem de ativação

1. Obter confirmação final para ampliar o acesso aos dados financeiros compartilhados, exigida pelo controle do navegador.
2. Conferir e publicar o arquivo firestore.rules no projeto Firebase gebon-portal-financeiro. Não publicar regras de outros projetos.
3. Publicar index.html desta branch em main de DRE-semanal e a branch de mesmo nome em main de financeiro.
4. Conferir os dois deploys do GitHub Pages. Recarregar abas antigas, que não podem continuar gravando no modelo separado.

O deploy intermediário sem os novos perfis foi rejeitado pela revisão automática. O main permaneceu intacto. Publicar somente o conjunto compartilhado completo.
