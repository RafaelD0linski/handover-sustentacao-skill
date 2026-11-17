# handover-sustentacao

Skill para o Claude que cria ou completa o **documento de Handover** (passagem de uma mudança/CHG para a equipe de sustentação) em .docx, no modelo da sua empresa.

## O que ela faz
- Usa um handover anterior como modelo e preserva o layout (estilos, tabelas, logotipo).
- Preenche identificação, descrição do sistema, o que mudou, fora do escopo, defeitos conhecidos, monitoração, versionamento (SVN/Git) e procedimentos.
- Lê o código, o diff e o `svn info` para apontar classes, métodos e branches.
- Não deixa campo vazio: pergunta o que falta ou marca como `PENDENTE` e diz onde achar.
- Nunca inventa URL, branch, CHG ou nomes, nem coloca dados sensíveis no documento.

## Como instalar
1. Baixe a pasta `handover-sustentacao/` (ou compacte em .zip).
2. No Claude, vá em **Settings → Capabilities → Skills** e envie o arquivo.
3. Peça: "faz o handover do sistema X" e anexe um handover antigo e o que tiver da mudança.

## Estrutura
```
handover-sustentacao/
└── SKILL.md
```

## Licença
MIT
