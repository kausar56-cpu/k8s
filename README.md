How to login GitHub 

GitHub Enterprise URL उघडतो.
"Sign in with SSO" किंवा "Continue with Okta" वर क्लिक करतो.
Okta login page उघडते.
Company email + password टाकतो.
MFA (Authenticator App) approve करतो.
परत GitHub मध्ये login होतो.
-------------------------------------------

Diagram flow

1. main branch वरून नवीन feature branch तयार कर
        │
        ▼
2. feature branch वर code लिही
        │
        ▼
3. git add .
        │
        ▼
4. git commit -m "Added login feature"
        │
        ▼
5. git push origin feature/login
        │
        ▼
6. GitHub वर Pull Request तयार कर
   (feature/login → main)
        │
        ▼
7. Team Lead / Reviewer code review करतो
   + CI/CD pipeline (build, test, security checks) चालते
        │
        ▼
8. सर्व checks ✅ Green आणि PR approve
        │
        ▼
9. Merge into main
        │
        ▼
10. Feature branch delete

11. ---------------------------------------
