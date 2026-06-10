---
name: MASAR (مَسَار)
colors:
  surface: '#faf8ff'
  surface-dim: '#d2d9f4'
  surface-bright: '#faf8ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f2f3ff'
  surface-container: '#eaedff'
  surface-container-high: '#e1e7ff'
  surface-container-highest: '#dae2fc'
  on-surface: '#131b2e'
  on-surface-variant: '#434655'
  inverse-surface: '#283044'
  inverse-on-surface: '#eef0ff'
  outline: '#737686'
  outline-variant: '#c3c6d7'
  surface-tint: '#0053db'
  primary: '#004ac6'
  on-primary: '#ffffff'
  primary-container: '#2563eb'
  on-primary-container: '#eeefff'
  inverse-primary: '#b4c5ff'
  secondary: '#006a63'
  on-secondary: '#ffffff'
  secondary-container: '#99efe5'
  on-secondary-container: '#006f67'
  tertiary: '#6a1edb'
  on-tertiary: '#ffffff'
  tertiary-container: '#8343f4'
  on-tertiary-container: '#f7edff'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#dbe1ff'
  primary-fixed-dim: '#b4c5ff'
  on-primary-fixed: '#00174b'
  on-primary-fixed-variant: '#003ea8'
  secondary-fixed: '#9cf2e8'
  secondary-fixed-dim: '#80d5cb'
  on-secondary-fixed: '#00201d'
  on-secondary-fixed-variant: '#00504a'
  tertiary-fixed: '#eaddff'
  tertiary-fixed-dim: '#d2bbff'
  on-tertiary-fixed: '#25005a'
  on-tertiary-fixed-variant: '#5a00c6'
  background: '#faf8ff'
  on-background: '#131b2e'
  surface-variant: '#dae2fc'
typography:
  display:
    fontFamily: Tajawal
    fontSize: 48px
    fontWeight: '700'
    lineHeight: '1.2'
  h1:
    fontFamily: Tajawal
    fontSize: 36px
    fontWeight: '700'
    lineHeight: '1.3'
  h2:
    fontFamily: Tajawal
    fontSize: 30px
    fontWeight: '700'
    lineHeight: '1.4'
  h3:
    fontFamily: Tajawal
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.4'
  h4:
    fontFamily: Tajawal
    fontSize: 20px
    fontWeight: '600'
    lineHeight: '1.4'
  body-lg:
    fontFamily: Tajawal
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.7'
  body:
    fontFamily: Tajawal
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.6'
  small:
    fontFamily: Tajawal
    fontSize: 14px
    fontWeight: '500'
    lineHeight: '1.5'
  caption:
    fontFamily: Tajawal
    fontSize: 12px
    fontWeight: '400'
    lineHeight: '1.4'
  english-body:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.5'
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  base: 8px
  gutter: 24px
  margin-desktop: 48px
  margin-tablet: 32px
  margin-mobile: 16px
  section-y-desktop: 96px
  container-max: 1280px
---

# MASAR Design System

## 1. Brand & Product Direction

MASAR is a smart operations workspace for organizations. It helps institutions create a private workspace, organize records, activate modules, manage users and access, follow workflows, improve data quality, and generate reports from one secure system.

MASAR should not look like a charity-only website. Humanitarian and NGO work is one important use case, but the visual identity should be broad enough for organizations, institutions, operational teams, field teams, and administrative teams.

The visual story is based on the meaning of the name “مَسَار”: direction, path, flow, and structured movement.

The product should feel:

- Professional
- Calm
- Trustworthy
- Smart
- Organized
- Arabic-first
- Operational
- Human-centered
- Secure without feeling heavy

Avoid generic SaaS templates. MASAR should feel like a real system that turns scattered organizational work into a structured path.

## 2. Visual Narrative

The MASAR interface should communicate:

Scattered work → organized workspace  
Unclear processes → visible workflows  
Separate tools → connected modules  
Raw data → trusted records  
Manual reporting → reviewable smart reports  
Uncontrolled access → secure private workspace

Use visual metaphors such as:

- paths
- connected nodes
- module boards
- pipelines
- workspace maps
- status chips
- timeline flows
- protected workspace diagrams

Do not overuse generic feature cards. MASAR’s design should explain value through product-like visuals, not only text blocks.

## 3. Color Usage

### Primary Blue

Use Primary Blue `#2563EB` for:

- main CTAs
- active states
- selected navigation
- important links
- primary progress indicators
- key workspace actions

### Deep Blue

Use `#004AC6` or `#0B5CD7` for:

- hover states
- stronger primary buttons
- hero emphasis
- high-importance actions

### Teal

Use Teal `#0F766E` for:

- successful operational states
- field-related workflows
- human-centered progress
- positive confirmation
- secondary accents

### AI Purple

Use AI Purple `#7C3AED` carefully for:

- AI-assisted duplicate detection
- smart suggestions
- automated report drafting
- intelligent insights
- report-generation states

AI should feel supportive, not dominant. MASAR is an operations platform enhanced by AI, not an AI gimmick.

### Backgrounds

Use:

- `#FAF8FF` for soft branded page backgrounds
- `#F8FAFC` for clean dashboard backgrounds
- `#FFFFFF` for cards, forms, panels, and modals
- `#0F172A` for premium trust/security sections

### Accessibility

Maintain strong contrast:

- body text should use `#131B2E`
- secondary text should usually use `#64748B`
- avoid using very pale gray for important Arabic copy
- primary buttons should always use white text

## 4. Typography

MASAR is Arabic-first.

Use **Tajawal** for:

- Arabic headings
- Arabic body text
- Arabic labels
- Arabic buttons
- Arabic navigation
- Arabic dashboard UI

Use **Inter** only for:

- English fallback text
- emails
- code-like values
- Latin data
- technical identifiers

Arabic line-height should be slightly more generous than English to improve readability.

Recommended usage:

- Hero title: 48px / 700
- Page H1: 36px / 700
- Section title: 30px / 700
- Card title: 20–24px / 600
- Body text: 16px / 400
- Helper text: 14px / 400–500
- Caption: 12px / 400

Do not make Arabic subtitles too small or too light. MASAR is operational, so clarity matters more than decoration.

## 5. Layout & Spacing

Use a strict 8px spacing system.

Desktop:

- max container: 1280px
- outer margin: 48px
- section vertical spacing: 96px
- grid: 12 columns, 24px gutter

Tablet:

- outer margin: 32px
- grid: 8 columns

Mobile:

- outer margin: 16px
- grid: 4 columns
- stack forms and modules vertically

RTL rules:

- navigation starts from the right
- logo is usually placed on the right
- primary content aligns to the right
- sidebars appear on the right in Arabic dashboards
- icons inside inputs should mirror correctly in RTL
- progress flows should move right-to-left unless the visual metaphor clearly requires otherwise

## 6. Elevation & Depth

MASAR uses tonal layering and soft elevation.

Level 0 — Page background:

- `#FAF8FF` or `#F8FAFC`

Level 1 — Cards and panels:

- white `#FFFFFF`
- 1px border `#E2E8F0`
- no heavy shadow

Level 2 — Interactive hover:

- soft shadow: `0px 4px 12px rgba(15, 23, 42, 0.05)`

Level 3 — Important panels/modals:

- shadow: `0px 12px 32px rgba(15, 23, 42, 0.10)`

Hero/CTA glow:

- soft blue, teal, or purple gradient glow
- should feel premium and calm, not flashy

## 7. Shape Language

MASAR should feel approachable but structured.

Use:

- Cards/containers: 16px–20px radius
- Inputs/buttons: 12px radius
- Pills/chips/badges: full radius
- Large CTA blocks: 24px radius
- Modals: 20px–24px radius

Avoid sharp enterprise corners unless used in dense data tables.

## 8. Buttons & Controls

### Primary Button

- background: `#2563EB`
- text: white
- radius: 12px
- height: 44px–52px
- hover: deeper blue
- use for main actions such as:
  - سجّل مؤسستك
  - إنشاء مساحة العمل
  - تسجيل الدخول
  - الانتقال إلى لوحة التحكم

### Secondary Button

- white background
- border: `#E2E8F0`
- text: `#131B2E`
- hover: soft blue background

### Teal Button

Use for secondary positive operational actions such as:

- إضافة متطوع
- تأكيد حضور
- حفظ توزيع

### AI Action Button

Use purple accent only for:

- توليد تقرير
- فحص التشابه
- اقتراح ذكي

### Disabled State

- low opacity
- no strong shadow
- clear disabled cursor/visual

## 9. Inputs & Forms

Form fields:

- height: 48px–56px
- radius: 12px
- border: `#E2E8F0`
- background: white
- focus border: `#2563EB`
- focus glow: soft blue ring
- error border: `#DC2626`
- success border: `#16A34A`

Use clear labels above fields.

Arabic input alignment:

- Arabic text aligned right
- icons placed appropriately for RTL
- email fields may keep Latin text LTR inside while the label remains RTL

Common auth/signup fields:

- اسم المؤسسة
- البريد الإلكتروني للمؤسسة
- رقم الجوال
- المنطقة
- كلمة المرور
- تأكيد كلمة المرور

Password fields:

- include show/hide icon
- include password strength indicator when needed
- use Arabic helper checklist

Validation messages:

- short
- specific
- Arabic
- placed close to the field

Examples:

- يرجى إدخال اسم المؤسسة.
- يرجى إدخال بريد إلكتروني صحيح.
- كلمتا المرور غير متطابقتين.
- كلمة المرور ضعيفة.
- هذا البريد مستخدم بالفعل.

## 10. Workspace & Multi-Organization Concept

MASAR gives each organization a private workspace.

Do not expose technical terms such as:

- tenant
- tenant_id
- schema
- database isolation
- multi-tenancy

Use user-friendly wording:

- مساحة عمل خاصة بمؤسستك
- مساحة عمل المؤسسة
- رابط مساحة العمل
- إعداد مساحة العمل
- تفعيل مساحة العمل

In registration screens, it is acceptable to show a lightweight workspace preview:

سيتم إنشاء مساحة عمل خاصة بمؤسستك  
masar.com/company-name

This preview should look like an info panel, not a required input field.

## 11. Modules

When MASAR says “modules,” it means real system modules, not small features.

The four MVP core modules are:

### 1. تقنية المعلومات والإدارة

Focus:  
إدارة الدخول، المستخدمين، الصلاحيات، وإعدادات المؤسسة.

### 2. العمليات الميدانية

Focus:  
إدارة السجلات الميدانية، البحث، كشف التشابه، والتوزيعات.

### 3. الموارد البشرية والمتطوعين

Focus:  
إدارة المتطوعين، الورديات، الحضور، وساعات العمل.

### 4. المتابعة والتقييم والتقارير

Focus:  
إدارة المهام، متابعة سير العمل، المؤشرات، والتقارير الذكية.

Landing page module section should show:

- الوحدات الأساسية
- exactly these four core module cards
- optional modules as separate future/additional modules, not random features

Optional/future modules may include:

- إدارة المخزون
- إدارة التمويل
- إدارة الشراكات
- إدارة الطلبات
- وحدة مخصصة

Do not represent modules as tiny toggles like “بحث” or “تحليلات”. Those are features, not modules.

## 12. Cards & Panels

Use cards for:

- modules
- status summaries
- dashboard KPIs
- form containers
- review blocks
- setup checklist items

Card style:

- white background
- 16px–20px radius
- 1px border
- soft hover shadow only if interactive

Module cards:

- icon
- title
- one-line description
- badge: أساسية / اختيارية / مفعّلة
- clear module identity

Dashboard KPI cards:

- may use thin top border in blue/teal/purple
- keep numbers large and readable
- avoid decorative clutter

AI insight cards:

- use subtle purple tint or glow
- label clearly as smart/AI-assisted
- keep explanation grounded

## 13. Tables & Dense Data

Tables are important for operations.

Rules:

- sticky headers for long tables
- 12px vertical cell padding for dense views
- clear row hover
- server-side pagination controls
- visible search and filter area
- masked sensitive fields where needed
- status badges for states

Arabic table alignment:

- text right-aligned
- numeric values can be aligned consistently
- actions should be easy to scan

## 14. Feedback & States

### Toasts

For RTL dashboards, use bottom-left or top-left placement when a right sidebar exists. Avoid covering right-side navigation.

### Alerts

Use inline alerts for form-level errors:

- error: red border and soft red background
- success: green border and soft green background
- info: blue border and soft blue background
- warning: amber border and soft warning background

### Empty States

Use simple monochrome or low-color illustrations. Keep focus on the next action.

Examples:

- لا توجد بيانات بعد.
- ابدأ بإعداد مساحة العمل.
- لم يتم تفعيل أي وحدة إضافية بعد.

### Loading States

Use:

- button loading text
- small spinner
- skeleton loading for tables/cards
- never leave users without feedback

## 15. Landing Page Rules

The landing page should tell a product story:

1. Hero: كل عمليات مؤسستك في مَسَار واحد
2. Problem: عندما يكبر العمل، تتشتت الصورة
3. Before/After: قبل مَسَار وبعده
4. Work Flow: كيف يرتّب مَسَار العمل؟
5. Modules: ابنِ مساحة عملك من وحدات مَسَار
6. Data/Workflow: بيانات أوضح، عمل أسهل
7. Security: مساحة عمل خاصة وآمنة لمؤسستك
8. CTA: ابدأ بتنظيم مؤسستك في مَسَار
9. Footer

Use:

- path visuals
- connected module cards
- before/after comparison
- pipelines
- workflow paths
- protected workspace diagram

Avoid:

- generic feature grids
- meaningless desktop/mobile screenshots
- charity-only wording
- very long marketing paragraphs

## 16. Authentication & Signup Screens

The approved organization signup flow is simple.

Fields:

- اسم المؤسسة
- البريد الإلكتروني للمؤسسة
- رقم الجوال
- المنطقة
- كلمة المرور
- تأكيد كلمة المرور

After signup:

- send verification link to organization email
- show “تحقق من بريد المؤسسة”
- no OTP boxes
- account/workspace inactive until email is verified
- after verification, admin enters first dashboard welcome/setup state

Signup action:

- إنشاء مساحة العمل

Email verification wording:

تم إنشاء مساحة عمل مؤسستك مبدئيًا. أرسلنا رابط تفعيل إلى البريد الإلكتروني الخاص بالمؤسسة.

Success wording:

تم تفعيل البريد بنجاح. أصبحت مساحة عمل مؤسستك جاهزة الآن.

## 17. Dashboard First-Time State

After verification, show a setup-focused dashboard, not fake heavy data.

Dashboard welcome title:

مرحبًا بك في مساحة عمل مؤسستك

Subtitle:

ابدأ بإعداد الوحدات وإضافة الفريق لتنظيم العمل داخل مَسَار.

Setup checklist:

- إكمال بيانات المؤسسة
- تفعيل الوحدات المناسبة
- إضافة أعضاء الفريق
- ضبط الصلاحيات
- البدء بإدارة السجلات والمهام

Status cards:

- حالة الحساب: مفعّل
- البريد الإلكتروني: تم التحقق
- مساحة العمل: جاهزة للإعداد

## 18. Accessibility & Usability

MASAR is used by operational and administrative users, so clarity matters.

Rules:

- maintain WCAG AA contrast
- do not rely on color alone
- use icons with labels
- keep buttons large enough
- use clear Arabic validation
- keep navigation predictable
- avoid unnecessary animation
- do not overload screens with decorative visuals

## 19. Stitch AI Generation Instructions

When generating MASAR screens in Stitch AI:

- Design high-fidelity Arabic RTL UI.
- Use MASAR design system exactly.
- Do not generate code.
- Prioritize layout, hierarchy, spacing, and product clarity.
- Use Tajawal for Arabic text.
- Keep components consistent across landing, auth, and dashboard.
- Use modules correctly as the four core MASAR modules.
- Keep the product broad for organizations, not humanitarian-only.
- Do not expose technical system terms.
- Make screens production-ready and not student-like.
