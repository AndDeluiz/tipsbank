# syntax=docker/dockerfile:1.7

# =============================================================================
# Imagem: chainguard/nginx:latest (roda como user 65532, nao-root por default).
# =============================================================================
FROM cgr.dev/chainguard/nginx:latest

EXPOSE 8080

# Configuracao do nginx (proxy reverso pras APIs)
COPY nginx.conf /etc/nginx/nginx.conf

# Arquivos estaticos do frontend
# Importante: os arquivos na maquina host precisam ter permissao 644 (legivel
# por outros) pro user 101 (nginx) conseguir ler. Docker COPY preserva perms.
COPY html/ /usr/share/nginx/html/

# USER 65532 (nginx) ja eh o default dessa imagem.
# USER 65532