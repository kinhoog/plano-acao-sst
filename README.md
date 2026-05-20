# Planos de Ação SST

Sistema web para criação, organização e acompanhamento de cronogramas de ações de Segurança e Saúde no Trabalho, voltado para documentos como PGR, PCMSO, LTCAT e rotinas internas de SST.

O projeto funciona em navegador, com interface em arquivo único (`index.html`) e sincronização de dados via Supabase.

## Funcionalidades

- Login com e-mail e senha via Supabase Auth.
- Cadastro público desativado: novos usuários devem ser criados manualmente no Supabase.
- Tela de perfis com foto, avatar, status online/offline e último acesso.
- Pastas por perfil para organizar planos de ação.
- Criação, duplicação, movimentação e exclusão de planos.
- Cronograma de ações com edição direta na tabela.
- Seções adicionais para equipamentos de emergência e treinamentos.
- Campos rich text com suporte a texto formatado e imagens.
- Busca, filtros e ações em lote.
- Exportação de relatório executivo em PDF.
- Exportação e importação de backup JSON.
- Modo dark/light com preferência local.
- Log de exclusões para perfil, pasta e plano de ação, mostrando quem executou a ação.
- Sincronização em tempo real entre usuários conectados.

## Estrutura

```text
.
├── index.html
└── README.md
```

O sistema foi mantido em um único arquivo HTML para facilitar publicação no GitHub Pages.

## Publicação no GitHub Pages

1. Crie um repositório no GitHub.
2. Envie o arquivo `index.html` para a raiz do repositório.
3. Envie também este `README.md`.
4. No GitHub, acesse `Settings > Pages`.
5. Selecione a branch principal e a pasta raiz.
6. Acesse o link gerado pelo GitHub Pages.

## Supabase

O sistema utiliza:

- Supabase Auth para login, alteração e redefinição de senha.
- Tabela `shared_states` para os dados compartilhados do sistema.
- Tabela `user_profiles` para exibição dos perfis públicos.
- Realtime para sincronização entre usuários.

Configuração recomendada:

- `Enable email provider`: ativado.
- `Allow new users to sign up`: desativado.
- Usuários criados manualmente em `Authentication > Users`.
- Row Level Security configurado conforme as políticas do projeto.

Importante: a chave usada no front-end deve ser somente a chave pública/publicável do Supabase. Nunca publique a `service_role key`.

## Uso

1. Entre com e-mail e senha de um usuário criado no Supabase.
2. Crie ou edite o perfil correspondente.
3. Abra um perfil para acessar as pastas.
4. Crie pastas e planos de ação.
5. Edite o cronograma, treinamentos e equipamentos diretamente nas tabelas.
6. Use `Exportar para PDF` para gerar o relatório executivo.
7. Use `Exportar JSON` para backup manual.
8. Use `Configurações > Consultar Log` para verificar exclusões registradas.

## Backup

O backup manual pode ser feito pelo botão `Exportar JSON`.

Para restaurar, use `Importar JSON`. Essa ação substitui os dados atuais após confirmação.

## Observações

- O sistema foi pensado para uso interno de uma equipe pequena de SST.
- Para muitos usuários simultâneos ou auditoria jurídica avançada, recomenda-se evoluir o banco para tabelas separadas por entidade e log dedicado.
- Imagens grandes em campos rich text podem aumentar o tamanho dos dados salvos. Prefira imagens objetivas e comprimidas.

## Créditos

- Idealização e estrutura inicial: Abner Rodrigues
- Evolução, testes e especificações adicionais: Erick Rocha
  
- Desenvolvimento assistido por IA: Codex / OpenAI
