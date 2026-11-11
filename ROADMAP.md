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
- Cadastro de funcionários existentes e verificados, perfis de gerente/atendente e permissões de catálogo/estoque aplicadas na API, com desativação de acesso por loja.
- ADM Vitruna global: CRUD inicial de planos, módulos, empresas, assinatura e recebimentos **manuais**.
- Testes de bloqueio por vencimento, suspensão, autorização global e isolamento entre lojas.
- **Aplicação efetiva do módulo `catalog`** no backend, tanto nas operações do lojista quanto na vitrine pública; módulos de outros recursos continuam pendentes.
- Edição manual dos módulos incluídos em planos, com alterações que afetam imediatamente as lojas assinantes.
- Documentação de manutenção e comentários nos arquivos mais importantes do sistema.

## Sem homologação / pendente

- Configuração e testes reais de SMTP, bucket e CDN.
- RLS no banco, role de execução restrita e política robusta de isolamento.
- MFA, auditoria das ações financeiras, convite de lojistas e gestão de operadores SaaS.
- Convites para funcionários sem conta prévia, auditoria de permissões e enforcement dos próximos módulos além de catálogo.
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
