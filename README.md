# public

托管静态服务
kubectl -n novoai exec deepcoach-backend-7bd94db75c-fpd8d -- sh -c '
printf "POSTGRES_AUTH_MODE=%s\n" "${POSTGRES_AUTH_MODE:-<unset>}"
printf "POSTGRES_USER=%s\n" "${POSTGRES_USER:-<unset>}"
printf "POSTGRES_HOST=%s\n" "${POSTGRES_HOST:-<unset>}"
printf "POSTGRES_DB=%s\n" "${POSTGRES_DB:-<unset>}"
printf "POSTGRES_SSL_MODE=%s\n" "${POSTGRES_SSL_MODE:-<unset>}"
printf "POSTGRES_ENTRA_SCOPE=%s\n" "${POSTGRES_ENTRA_SCOPE:-<unset>}"
printf "POSTGRES_ENTRA_AUTHORITY=%s\n" "${POSTGRES_ENTRA_AUTHORITY:-<unset>}"
printf "AZURE_CLIENT_ID=%s\n" "${AZURE_CLIENT_ID:-<unset>}"
printf "AZURE_TENANT_ID=%s\n" "${AZURE_TENANT_ID:-<unset>}"
printf "AZURE_FEDERATED_TOKEN_FILE=%s\n" "${AZURE_FEDERATED_TOKEN_FILE:-<unset>}"
'

kubectl -n novoai exec deepcoach-backend-7bd94db75c-fpd8d -- env \
| grep -E '^(POSTGRES_AUTH_MODE|POSTGRES_USER|POSTGRES_HOST|POSTGRES_DB|POSTGRES_SSL_MODE|POSTGRES_ENTRA_SCOPE|POSTGRES_ENTRA_AUTHORITY|AZURE_CLIENT_ID|AZURE_TENANT_ID|AZURE_FEDERATED_TOKEN_FILE)='

kubectl -n novoai exec <pod名> -- python -c '
import psycopg
from app.core.postgres_auth import get_postgres_connection_kwargs
conn = psycopg.connect(\*\*get_postgres_connection_kwargs(connect_timeout=5))
print(conn.execute("select current_user, current_database()").fetchone())
'
