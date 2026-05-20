# BPMN - Processo do Sistema Planos de Ação SST

Este arquivo único documenta o processo operacional do sistema, desde a criação do usuário no Supabase até a gestão dos planos de ação, sincronização, exportação e consulta de logs.

O GitHub renderiza o diagrama Mermaid abaixo como uma imagem visual diretamente no arquivo.

```mermaid
flowchart TB
  start((Início))

  subgraph admin["Administrador / Supabase"]
    A1["Criar usuário no Supabase"]
    A2["Definir e-mail e senha temporária"]
    A3["Manter cadastro público desativado"]
  end

  subgraph tecnico["Técnico SST"]
    T1["Acessar link do GitHub Pages"]
    T2["Informar e-mail e senha"]
    T3{"Login válido?"}
    T4["Alterar senha, se necessário"]
    T5["Selecionar perfil"]
    T6{"Perfil próprio ou compartilhado?"}
    T7["Criar/editar perfil próprio"]
    T8["Abrir perfil compartilhado"]
    T9["Criar ou selecionar pasta"]
    T10["Criar novo plano de ação"]
    T11{"Iniciar como?"}
    T12["Carregar template padrão"]
    T13["Iniciar do zero"]
    T14["Editar cronograma de ações"]
    T15["Editar equipamentos e treinamentos"]
    T16["Inserir textos, imagens e observações"]
    T17["Filtrar, buscar e alterar status"]
    T18{"Precisa excluir algo?"}
    T19["Excluir perfil, pasta ou plano"]
    T20["Exportar PDF executivo"]
    T21["Exportar JSON de backup"]
    T22["Consultar log de exclusões"]
    T23["Sair do sistema"]
  end

  subgraph sistema["Sistema / Supabase"]
    S1["Validar autenticação"]
    S2["Carregar dados compartilhados"]
    S3["Publicar/atualizar perfil público"]
    S4["Sincronizar presença online/offline"]
    S5["Salvar alterações automaticamente"]
    S6["Mesclar alterações por perfil, plano e linha"]
    S7["Sincronizar dados em tempo real"]
    S8["Registrar log de exclusão com usuário responsável"]
    S9["Gerar PDF"]
    S10["Gerar arquivo JSON"]
    S11["Encerrar sessão"]
  end

  fim((Fim))

  start --> A1 --> A2 --> A3 --> T1
  T1 --> T2 --> S1 --> T3
  T3 -- "Não" --> T2
  T3 -- "Sim" --> S2 --> S3 --> S4 --> T4
  T4 --> T5
  T5 --> T6
  T6 -- "Próprio" --> T7 --> S5
  T6 -- "Compartilhado" --> T8
  S5 --> T9
  T8 --> T9
  T9 --> T10
  T10 --> T11
  T11 -- "Template" --> T12
  T11 -- "Zero" --> T13
  T12 --> T14
  T13 --> T14
  T14 --> T15 --> T16 --> T17
  T17 --> S5 --> S6 --> S7
  S7 --> T18
  T18 -- "Sim" --> T19 --> S8 --> S7
  T18 -- "Não" --> T20
  T20 --> S9 --> T21
  T21 --> S10 --> T22
  T22 --> T23 --> S11 --> fim
```

## Regras Do Processo

- O administrador cria usuários diretamente no Supabase.
- O cadastro público fica desativado.
- O técnico acessa o sistema apenas com e-mail e senha autorizados.
- Todos os perfis são visíveis para a equipe.
- Qualquer técnico pode abrir perfis compartilhados para trabalho.
- Edição/exclusão de perfil exige confirmação protegida.
- Alteração de senha exige senha atual.
- Alterações são salvas automaticamente e sincronizadas em tempo real.
- Exclusões de perfil, pasta e plano são registradas em log.
- PDF executivo e backup JSON podem ser gerados pelo próprio sistema.

## Benefícios Do Processo

- Centraliza os cronogramas de ação de SST.
- Reduz uso de planilhas soltas.
- Padroniza a criação de planos por template.
- Melhora rastreabilidade de exclusões.
- Permite trabalho compartilhado entre técnicos.
- Mantém backup manual via JSON.
- Gera relatório executivo em PDF para documentação.

## Versão Curta Para Apresentação

O processo parte de usuários criados manualmente no Supabase, com cadastro público bloqueado. O técnico acessa o sistema, seleciona um perfil, organiza pastas, cria planos de ação e edita cronogramas de SST com salvamento automático. O sistema sincroniza os dados em tempo real, gera PDF/JSON e registra em log as exclusões de perfil, pasta e plano, informando qual usuário executou a ação.
