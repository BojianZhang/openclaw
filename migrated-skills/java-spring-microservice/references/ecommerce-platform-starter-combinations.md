# E-commerce Platform Starter Combinations

Use this file when the user wants staged starter combinations for a modular Java shopping platform rather than starting with the full 乐SHOP capability set.

These combinations are meant for gradual self-built projects.

## Combination A: Common + Portal + Manager

### Best for
- first modular shopping-platform baseline
- separating user-facing and admin-facing concerns early

### Modules
- `shop-common`
- `shop-portal`
- `shop-manager`

### Why this is a good first combo
It establishes the two most visible platform boundaries without forcing identity/order/payment complexity too early.

### Upgrade path
- add SSO when identity reuse becomes real
- add Redis when hot/state access pressure appears

## Combination B: Common + Portal + SSO

### Best for
- when unified identity/session handling becomes important before order complexity grows

### Modules
- `shop-common`
- `shop-portal`
- `shop-sso`

### Why this combo matters
It teaches that identity is a capability boundary, not just a login page inside portal.

### Upgrade path
- add Redis for session/state acceleration
- later add manager or order depending on business pressure

## Combination C: Common + Portal + SSO + Redis

### Best for
- when portal and identity flows already have hot-read/state pressure

### Modules
- `shop-common`
- `shop-portal`
- `shop-sso`
- Redis support

### Why this combo matters
It is a practical platform-performance step without yet introducing search or payment complexity.

## Combination D: Common + Portal + Order + SSO

### Best for
- when shopping flow and transaction intent have become clearer than admin complexity

### Modules
- `shop-common`
- `shop-portal`
- `shop-order`
- `shop-sso`

### Why this combo matters
It creates the basic user -> identity -> order chain before payment integration arrives.

### Upgrade path
- add Redis if order/session pressure appears
- add payment only after order truth is stable

## Combination E: Common + Portal + Search (ES)

### Best for
- when retrieval/search experience is becoming more important than transaction closure

### Modules
- `shop-common`
- `shop-portal`
- search capability (ES)

### Why this combo matters
It keeps search as a user-experience capability, not a mandatory part of the very first platform baseline.

## Combination F: Common + Portal + Order + Payment

### Best for
- when the platform already has stable order boundaries and now needs external settlement

### Modules
- `shop-common`
- `shop-portal`
- `shop-order`
- payment integration

### Why this combo should come later
Payment is cleaner once order truth already exists.

## Combination G: Common + Portal + SSO + SMS

### Best for
- when identity/verification trust requirements appear before heavy transaction closure complexity

### Modules
- `shop-common`
- `shop-portal`
- `shop-sso`
- SMS capability

### Why this combo matters
It treats SMS as verification support for identity/risk-sensitive flows, not as a core domain by itself.

## Combination H: Common + Portal + Manager + SSO + Order

### Best for
- when the platform is becoming a more complete shopping system with user, admin, identity, and order boundaries all active

### Modules
- `shop-common`
- `shop-portal`
- `shop-manager`
- `shop-sso`
- `shop-order`

### Why this is a strong medium-stage combo
It captures the major platform role boundaries before pulling in every support capability.

## Recommended adoption order

For a gradual self-built commerce platform, a reasonable path is:
1. **A** Common + Portal + Manager
2. **B** or **D** depending on whether identity or order pressure appears first
3. **C** when Redis/state pressure becomes real
4. **E** when search experience matters
5. **F** when order truth is stable enough for payment integration
6. **G** when stronger verification becomes necessary
7. **H** when the platform is mature enough to hold the main business boundaries together

## Anti-overengineering reminder

Do not start with portal + manager + sso + order + payment + sms + redis + es + cloud storage all at once.
A better platform grows by visible user-flow and operational pressure.
