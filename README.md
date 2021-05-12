vault write database/config/attendance \
  plugin_name=postgresql-database-plugin \
  allowed_roles="developer" \
  connection_url="postgresql://{{username}}:{{password}}@postgres:5432?sslmode=disable" \
  username="postgres" \
  password="password"

vault write database/roles/developer \
    db_name=attendance \
    creation_statements="CREATE ROLE \"{{name}}\" WITH LOGIN PASSWORD '{{password}}' VALID UNTIL '{{expiration}}'; \
        GRANT SELECT ON ALL TABLES IN SCHEMA public TO \"{{name}}\";" \
    default_ttl="1h" \
    max_ttl="24h"

vault read database/creds/developer