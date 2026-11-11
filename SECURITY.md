# Política de segurança

A segurança não é garantida pela separação dos repositórios: depende de controles técnicos efetivos e testes.

## Controles incluídos na fundação inicial
- Senhas Argon2id.
- Sessões opacas: token no cookie HttpOnly/SameSite=Lax e somente hash no banco.
- Restrição de CORS e verificação Origin em requisições mutáveis.
- Rate limiting, validação Zod no cadastro/login/verificação.
- Não conceder SUPERADMIN no cadastro.
- Lojas resolvidas por associação de usuário autenticado.

## Pendências bloqueadoras para produção
- Provedor real de e-mail e fluxos de recuperação/reenvio; validações de domínio SMTP.
- MFA para operadores SaaS; rotinas auditadas de administração.
- RLS por tenant e papel restrito no banco; migrações versionadas.
- Testes E2E contra PostgreSQL real, testes de isolamento com usuários de lojas distintas.
- Testes de CSRF, CORS, autorização, sessão expirada, upload, rate limiting e concorrência.
- Secret manager, HTTPS e reverse proxy com política correta de `trust proxy`.
- Backups criptografados e testes de restauração.
- Pipeline CI de build/test/lint e varredura de dependências.
- Observabilidade sem vazamento de PII, LGPD, política de retenção e revisão por profissional de segurança.
- Proteções contra enumeração de usuários, abuso, bots, notificações e robustez de fluxo de assinatura.

## Ambientes

Nunca disponibilizar credenciais do docker-compose em produção. Nunca comitar `.env`, tokens, cookies ou credenciais reais. Ativar `COOKIE_SECURE` em produção. Configurar o domínio de frontend, domínio de API, CORS e cookies conforme a hospedagem final.
