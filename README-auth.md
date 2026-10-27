# Correção do cadastro do DRIFT no dashboard real

O `app.py` inicia o `start_web_dashboard()` do `dashboard_server.py`. O problema era que o dashboard registrava apenas as páginas HTML: não havia rotas para `/api/auth/signup`, `/api/auth/login` e `/api/me`, nem rota para servir `login.js`, `shared.js` e `shared.css`.

Esta versão adiciona:

- cadastro e login usando SQLite;
- sessão local via cookie `ffglory_session`;
- endpoint de sessão `/api/me`;
- logout e troca de senha;
- rota para arquivos estáticos da pasta `DRIFT`;
- bypass do Turnstile somente em localhost;
- conta inicial de desenvolvimento.

Conta de teste:

```text
Usuário: demo
Senha: Demo1234!
```

O banco `ffglory_auth.db` é criado no diretório do `app.py`. As senhas são armazenadas com PBKDF2-HMAC-SHA256, nunca em texto puro.

Execute o bot como você já executava. O dashboard continuará na porta configurada pelo `app.py` (no arquivo enviado, `20333`):

```text
http://localhost:20333/login
```

Esta autenticação é adequada para desenvolvimento local. Antes de publicar, configure HTTPS, sessões persistentes/expiráveis, proteção CSRF, rate limiting e Turnstile real.
