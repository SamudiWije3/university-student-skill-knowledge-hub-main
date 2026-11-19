# Faculty Approval - VS Code setup

1. Back up your Supabase database. Open this folder in VS Code and serve it over localhost (Live Server).
2. In Supabase SQL Editor run `faculty-approval-migration.sql` **after** the original database schema is installed. Test first on a copy of your project.
3. Create an admin account in Supabase Authentication, then insert its UUID as `super_admin` using the commented SQL statement at the end of the migration. Add faculty admins the same way with role `faculty_admin` and the **exact** faculty string used by registration.
4. Review old students: migration marks profiles without an approval status as `pending` by default. Decide who should be approved before production.
5. Log in from `login.html` → Administrator Login. The admin approval list is in `admin-dashboard.html`.
6. **SECURITY TODO BEFORE REAL DEPLOYMENT:** Existing project policies still allow authenticated writes to posts, resources, articles, likes, bookings, and storage. Replace those policies with checks using `public.is_approved_student()`, plus correct ownership checks. Also replace browser-local/mock user flows with verified Supabase auth, and audit old admin management functions. The read-only banner is UI guidance, not a security boundary. Do not treat this as a production-complete access-control implementation.
7. Test pending/approved/rejected accounts, cross-faculty approvals, anonymous access, and direct REST API write attempts.


## Integration into the latest uploaded project
This package is based on `university-student-skill-knowledge-hub-main.zip`, preserving its dashboard, metrics, and other existing files. The administrator login link is on login.html, not index.html or dashboard.html.

**Important limitations:** This is an integration starter, not a fully secured read-only platform. Existing RLS policies for posting, booking, uploads, and other writes still require review and replacement. The admin user/resource/article management screens contain legacy browser-local functionality; they must not be treated as secure production moderation. The original registration form does not yet show an explicit approval-status page. The database approval workflow requires existing schema and Supabase deployment. Test with a backup Supabase project first.