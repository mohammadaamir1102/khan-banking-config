# banking config repository

This folder is the **content of the Git-backed Config Server repository**.

- Upstream: `https://github.com/mohammadaamir1102/khan-banking-config.git`
- Branch: `main`
- It is also initialised as its own Git repo here (`config-repo/.git`).

## File naming rule
Config Server resolves files by `spring.application.name` and active profile:

| File | Applies to |
|---|---|
| `application.yml` | every service (base) |
| `application-<profile>.yml` | every service for that profile |
| `<service>.yml` | that service |
| `<service>-<profile>.yml` | that service for that profile |

> The name must match `spring.application.name` exactly. `api-gateway.yml` (not `gateway.yml`),
> `user-management-service.yml`, etc.

## Local development
Config Server runs with the `native` profile and reads this folder from disk. No push needed.

## Production / shared environments
Push this folder to Git and run Config Server with the `git` profile:
```bash
git push -u origin main
# then, when starting config-server:
CONFIG_PROFILE=git \
CONFIG_GIT_URI=https://github.com/mohammadaamir1102/khan-banking-config.git \
java -jar config-server.jar
```

## Secrets
This repository contains **no secrets** — only placeholders and non-sensitive values. Passwords
and admin credentials are supplied as environment variables / Kubernetes Secrets.
