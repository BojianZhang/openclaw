# E-commerce Platform Minimal Skeletons

Use this file when the user wants the smallest reusable module skeletons for a modular Java shopping platform.

These are repo-level starter skeletons, not full production blueprints.

## 1. Common module skeleton

### Role
Shared DTOs, wrappers, enums, utilities, basic cross-module support.

### Minimal contents
```text
shop-common/
  src/main/java/
    dto/
    vo/
    enums/
    utils/
    result/
```

### Avoid
- order business logic
- search implementation
- login business flow

## 2. Portal module skeleton

### Role
User-facing shopping flow entry.

### Minimal contents
```text
shop-portal/
  controller/
  service/
  templates or web views/
  config/
```

### Typical dependencies
- common
- web/view layer
- optional rpc/sso integration later

## 3. Manager module skeleton

### Role
Admin/operations-facing workflow entry.

### Minimal contents
```text
shop-manager/
  controller/
  service/
  templates/
  config/
```

### Typical dependencies
- common
- web/view layer
- persistence support

## 4. SSO module skeleton

### Role
Identity/session/token capability.

### Minimal contents
```text
shop-sso/
  controller/
  service/
  repository or mapper/
  config/
```

### Typical dependencies
- common
- persistence support
- optional Redis support

## 5. Order module skeleton

### Role
Order creation/query/state flow.

### Minimal contents
```text
shop-order/
  controller/
  service/
  mapper or repository/
  config/
```

### Typical dependencies
- common
- sso
- persistence support
- payment integration later

## 6. RPC contract module skeleton

### Role
Shared interfaces and collaboration seams.

### Minimal contents
```text
shop-rpc/
  api/
  dto/
  service-contract/
```

### Avoid
- concrete business implementations

## 7. Support capability attachment rule

Treat these as attachments that join the main module skeletons later:
- Redis
- Elasticsearch
- payment integration
- SMS verification
- cloud storage

Do not make every one of them a top-level business module on day one unless the project truly needs that boundary.

## Recommended initial skeleton

```text
shop-root/
  pom.xml
  shop-common/
  shop-portal/
  shop-manager/
```

## Recommended next skeleton

```text
shop-root/
  shop-common/
  shop-portal/
  shop-manager/
  shop-sso/
  shop-order/
  shop-rpc/
```

## Source notes

Generalized from the user's 乐SHOP project structure into reusable minimal platform skeletons.
