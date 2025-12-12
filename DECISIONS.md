# Technical decisions

## Why Flutter?
- Single codebase for iOS and Android
- Fast UI iteration
- Long-term scalability for a commercial product

## Why is the source code private?
- Commercial intent
- Intellectual property protection
- The value lies in the final product, not in isolated code snippets

## Modular tab-based structure
Each tab is treated as an independent module to:
- Improve maintainability
- Reduce coupling
- Allow feature-level scalability

## Review tab
Key architectural decision to separate:
- Static user data (Profile)
- Time-based progress data (Review)
