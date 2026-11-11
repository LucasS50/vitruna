# Roadmap Vitruna

## Fase 1 — fundação (em andamento)
1. Criar repositórios e branches separadas (**feito**).
2. Código inicial NestJS, Prisma, PostgreSQL e endpoints de conta/loja (**feito, não homologado**).
3. Base Next.js com landing, login/cadastro e dashboards iniciais (**feito, não homologado**).
4. Instalar dependências, gerar e executar migrações, realizar builds e testes (**pendente**).
5. E-mail transacional, onboarding seguro, recuperação de senha, ajustes de UX e CI (**pendente**).
6. RLS e testes cross-tenant com PostgreSQL real (**pendente**).
7. Abrir PRs após resultados de qualidade (**pendente**).

## Fase 2 — catálogo no painel do lojista
CRUD de produtos, categorias, imagens e variantes de tamanho/cor. Regras de estoque por variante, auditoria e permissões.

## Fase 3 — vitrine pública
Rotas por slug, página de produto, categorias, pesquisa/filtros, carrinho e solicitação de atendimento pelo WhatsApp. UX responsiva e SEO.

## Fase 4 — pedidos e estoque
Solicitações, status, histórico, atualização de estoque idempotente e indicadores operacionais reais.

## Fase 5 — gestão SaaS
Superadmin completo, lojas, planos, assinaturas, cobrança recorrente, bloqueios e relatórios.

## Fase 6 — preparação comercial
Testes funcionais e segurança, backups, monitoramento, políticas de privacidade, homologação com 3 lojas piloto e deploy.

## Aceite da Fase 1
- Backend e frontend instalam e constroem sem falha.
- Banco sobe no Docker e migrations funcionam.
- Cadastro -> verificação -> login -> sessão -> logout validado.
- Loja A não consulta os dados privados da Loja B, testado em E2E.
- Conta comum recebe 403 em `/admin/summary`.
- Cookies, Origin e expiração de sessão testados.
- Não há segredos comitados nem dados simulados apresentados como dados reais.
- Nenhuma mudança de desenvolvimento foi feita diretamente na main.
