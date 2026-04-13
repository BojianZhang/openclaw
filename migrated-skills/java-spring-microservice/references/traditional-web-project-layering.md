# Traditional Web Project Layering

Use this file when the user needs a clean explanation of classic Java Web project layering in a JSP/Servlet/DAO style project.

This reference is inspired by the 云日记 sample.

## Why this sample matters

Not every Java project starts with Spring Cloud, RPC, Redis, or MQ.
A classic Java Web project still teaches foundational ideas:
- request handling
- layering
- data-access abstraction
- session/cookie-based login state
- module-by-module business growth

## Canonical layering model

### 1. View layer
Typical technologies:
- JSP
- static resources
- frontend page templates

Responsibility:
- page rendering
- user input display/collection
- presenting data returned by backend layers

Important boundary:
- view should not own database logic

## 2. Web / controller layer
Typical forms:
- `HttpServlet`
- route/action-oriented servlet classes

Responsibility:
- receive requests
- parse parameters
- do basic validation/dispatch
- coordinate with service layer
- write JSON/page response or forward/redirect

Important boundary:
- servlet/controller should not directly become the home of repeated JDBC logic

## 3. Service layer
Responsibility:
- business rules
- multi-step workflow coordination
- validation beyond raw parameter parsing
- calling DAO/base data-access layer

Important boundary:
- service should express business flow, not page rendering details

## 4. DAO / BaseDao layer
Responsibility:
- database access
- query/update abstraction
- repeated JDBC code sinking

Why BaseDao matters:
- it demonstrates the first abstraction step in data-access design
- it prevents every module from hand-writing the same JDBC boilerplate repeatedly
- it is a useful stepping stone toward later repository/ORM understanding

## 5. Utility/support layer
Typical contents:
- DB util / JDBC util
- string/date helpers
- cookie/session helpers
- result wrappers / common response shapes

Important boundary:
- utility code should support modules, not quietly absorb business logic

## Typical functional module growth in the sample

A practical progression from the 云日记 sample is:
1. development flow and project setup
2. user login
3. BaseDao abstraction
4. homepage and免登录 handling
5. user module
6. type/category module
7. note module
8. homepage module
9. statistics/reporting

This is useful because it shows how a basic single-project system grows by business modules after foundational layers are in place.

## Session/Cookie note

Classic Java Web projects often express login state through session/cookie mechanisms.
This is valuable because it teaches state handling directly, before later frameworks abstract it away.

## Reporting/analytics note

Statistics/reporting modules are worth mentioning in small projects because they show:
- aggregation thinking
- data presentation beyond CRUD
- practical backend-to-frontend data shaping

## How to answer using this reference

Use this when the user asks:
- how should a traditional Java Web project be layered?
- what is the value of BaseDao?
- what can a simple JSP/Servlet project prove technically?
- how do small single-project systems grow functionally?

A strong answer should:
1. explain the classic layering clearly
2. emphasize repeated-code sinking into BaseDao/util layers
3. show module growth after foundational layers exist
4. avoid pretending this is a distributed-system architecture

## Source notes

Distilled from the user's 云日记 sample across development flow, login, BaseDao, homepage, user/type/note modules, and statistics/reporting stages.
