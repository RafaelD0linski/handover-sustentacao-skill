---
name: handover-sustentacao
description: Criar ou completar o documento de Handover (passagem para a sustentação) de uma mudança/CHG, em .docx no modelo da empresa, a partir do código, svn info e dados do projeto.
---

# Handover para a sustentação

Gera o documento de Handover de um sistema alterado numa mudança (CHG), pronto para entregar à sustentação, sem campos em branco.

## Quando usar
- "Faz o handover do sistema X", "cria o documento de passagem", "completa esse handover".
- O usuário manda um handover antigo, o código, um diff, a saída de `svn info` ou descreve a mudança.

## Saída
- Sempre **.docx no modelo da empresa** (é o formato que a sustentação recebe). Carregar a skill `docx` antes de montar o arquivo.
- Um arquivo por sistema: `Handover_<SISTEMA>_<CHG>.docx`.
- Se o usuário mandar um handover existente, **usar ele como modelo**: copiar o arquivo e substituir só o conteúdo, preservando estilos, tabelas, cabeçalho, rodapé e logotipo. Nunca recriar o layout do zero quando existe modelo.
- Se não houver modelo nesta conversa, pedir um handover anterior (qualquer sistema) antes de montar. Só sem modelo nenhum, usar a estrutura abaixo.

## Estrutura padrão (quando não há modelo)
1. **Identificação:** sistema, número da CHG, projeto, data de implantação, fim da garantia (implantação + 3 meses), gerente do projeto, responsável na sustentação, desenvolvedor.
2. **Descrição do sistema:** o que a aplicação faz, tipo (SOAP, REST, batch, EJB), tecnologias (ex.: Java, JasperReports, CICS, SQL Server, stored procedures) e principais serviços/endpoints.
3. **O que mudou:** regra de negócio implementada e onde no código (classe.método), em linguagem que a sustentação entenda.
4. **Fora do escopo:** o que NÃO foi alterado e por quê (ex.: endpoints de gravação, outro sistema responsável, mainframe de outra equipe, com o nome do responsável).
5. **Defeitos conhecidos / pontos de atenção:** divergências, massa de teste volátil, diferença entre nós do cluster etc.
6. **Monitoração pós-implantação:** o que olhar, onde (log, linha exata) e por quantos dias.
7. **Versionamento (SVN/Git):** URLs de Produção, Homologação e Desenvolvimento, no padrão `http://<servidor-svn>/svn/<repositorio>/branches/<branch>`. Produção pode ser N/A se for o padrão do time.
8. **Procedimentos:** build e deploy (ex.: via pipeline de IC/release), rollback e dependências.
9. **Contatos.**

## Como preencher
1. Ler tudo o que veio: modelo, código, diff, `svn info`, CHG, e-mails.
2. **Código:** localizar as classes e métodos alterados (grep pelo nome da regra) e descrever onde a regra é aplicada. Se tiver acesso à pasta do projeto, rodar `svn info` (linha `URL:`) e `svn log -l 10` (ou `git remote -v` e `git log -10`) para achar a branch e os commits.
3. **Dados comuns entre sistemas da mesma CHG** (datas, gerente, sustentação, regra) devem ser idênticos em todos os documentos; conferir isso.
4. **Nunca deixar campo vazio.** Se a informação não existe nos materiais:
   - perguntar ao usuário de uma vez só, listando tudo o que falta (ex.: "URL do SVN de Homologação do sistema X");
   - se ele não souber, preencher com `PENDENTE` destacado em amarelo e listar na resposta onde encontrar (`svn info` na pasta, Eclipse → Properties → SVN Info, configuração do job de IC).
   - Nunca inventar URL, nome de branch, CHG ou nome de pessoa.
5. **Segurança:** nunca colocar número de cartão completo, senha, token ou dado de cliente real no documento. Exemplos de cartão sempre mascarados (6 primeiros + X + 4 últimos).

## Conferência antes de entregar
- Converter o .docx para texto (`pandoc -t plain`) e checar: nenhum campo vazio, nenhum `<placeholder>` sobrando, CHG e datas iguais em todo o documento.
- Renderizar a primeira página em imagem e olhar se o layout do modelo se manteve.

## Resposta no chat
Curta: quais arquivos foram gerados, e uma lista só do que ficou `PENDENTE` e onde achar. Sem repetir o conteúdo do documento.
