# Vitruna — situação técnica e roadmap

A implementação está nas branches `dev/fase-1-fundacao` de frontend e backend. A `main` não é alterada até a revisão dos pull requests. **Código existente não significa produção homologada.**

## Entregue no código e em testes automatizados

- API NestJS + PostgreSQL/Prisma, migrações versionadas, autenticação por sessão HttpOnly e confirmação/recuperação via tokens.
- Landing page responsiva, cadastro e login dos administradores.
- Vitrine pública por slug, sem login do consumidor, catálogo, variantes, busca, filtros e carrinho local por loja.
- Mensagem de WhatsApp com carrinho e total estimado; sem pagamento ou registro automático de pedido.
- Painel do proprietário: produtos, estoque por SKU, fotografias, galeria e configuração de WhatsApp.
- Upload seguro de JPG/PNG/WebP para storage compatível com S3, **dependente de credenciais externas**.
- Dashboard do lojista com KPIs reais e personalização básica de cores/texto.
- Cadastro de funcionários, perfis de gerente/atendente e permissões de catálogo/estoque aplicadas na API, com desativação de acesso por loja.
- Convites por e-mail com expiração de 48 horas, cancelamento, aceite de conta existente e cadastro de funcionário novo sem criar loja; exige SMTP configurado.
- ADM Vitruna global: CRUD inicial de planos, módulos, empresas, assinatura e recebimentos **manuais**.
- Contratação e renovação interna com protocolo, solicitação vinculada ao lojista verificado, fila comercial, atendimento via WhatsApp e confirmação manual sem publicação automática.
- Exclusividade de solicitação aberta por loja garantida no PostgreSQL (índice parcial) e primeiros eventos de auditoria de finanças no ADM.
- Publicação pública exige período pago ou carência válida, mesmo que exista vencimento futuro cadastrado.
- Testes de bloqueio por vencimento, suspensão, autorização global e isolamento entre lojas.
- **Aplicação efetiva do módulo `catalog`** no backend, tanto nas operações do lojista quanto na vitrine pública; módulos de outros recursos continuam pendentes.
- Edição manual dos módulos incluídos em planos, com alterações que afetam imediatamente as lojas assinantes.
- Documentação de manutenção e comentários nos arquivos mais importantes do sistema.

## Sem homologação / pendente

- Configuração e testes reais de SMTP, bucket e CDN.
- RLS no banco, role de execução restrita e política robusta de isolamento.
- MFA, auditoria ampla das ações administrativas (auditoria financeira inicial entregue), convite de lojistas e gestão de operadores SaaS.
- Auditoria de convites/permissões, proteção contra abuso distribuído e enforcement dos próximos módulos além de catálogo.
- Testes ponta a ponta no navegador em ambiente completo com múltiplas empresas.
- Baixa de estoque auditada, pedidos internos confirmados, conciliação e reversão de pagamentos manuais.
- Upload de logotipos e banners, personalização avançada, contraste e acessibilidade.
- Limitação comercial/planos aprovada pelo proprietário da plataforma.
- Deploy, backups, monitoramento, LGPD, termos e privacidade.

## Regras de identidade

| Área | Banco | Pode acessar |
|---|---|---|
| ADM Vitruna | User.platformRole=SUPERADMIN | todas as empresas, planos, módulos e financeiro manual |
| Superadmin da loja | StoreMember.role=OWNER | somente sua própria loja |
| Equipe da loja | StoreMember.role=MANAGER/ATTENDANT | permissões restritas, ainda a detalhar |
| Consumidor | sem usuário | catálogo e carrinho sem autenticação |

## Qualidade e aceitação

- Migrations aplicáveis e builds no GitHub Actions.
- Testes unitários e PostgreSQL reais para isolamento de tenants.
- Homologação pelo navegador e revisão de segurança **ainda necessárias**.
- Não publicar credenciais nem ativar produção sem revisão de segurança.

## Critério de encerramento
Consulte [o roteiro de release no backend](https://github.com/LucasS50/vitruna-backend/blob/dev/fase-1-fundacao/docs/RELEASE_READINESS.md). Builds de GitHub Actions não substituem SMTP, storage, navegador real, HTTPS, backups, RLS e MFA validados no ambiente de produção.
