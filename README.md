# guidewire-hackathon

🛡️ GigShield — AI-Powered Parametric Insurance for India's Gig Economy

Guidewire DEVTrails 2026 | University Hackathon
Protecting food delivery partners from income loss caused by uncontrollable external disruptions.


🎬 Demo Video

📹 Watch our 2-minute strategy & prototype walkthrough → https://drive.google.com/file/d/1tT6jwGNurNwPH6sHIjpazx5cynz2hxeY/view?usp=drive_link


📌 The Problem
India's ~5 million food delivery partners (Zomato, Swiggy) lose 20–30% of their monthly income during external disruptions — heavy rain, heatwaves, floods, city-wide bandhs, and severe air pollution. They have no safety net. When disruptions hit, they bear the full financial loss alone.
GigShield solves this with a zero-touch, AI-powered parametric insurance platform. No claim forms. No disputes. Automatic payouts — within 30 minutes of a trigger event.

👤 Persona — Who We're Building For
Chosen Segment: Food Delivery Partners (Zomato / Swiggy)
Why Food Delivery?

Highest outdoor exposure — riders spend 4–8 hours daily on roads
Most sensitive to real-time weather (rain immediately halts deliveries)
Largest gig worker pool in India (~5 million active delivery partners)
Platform order volume drops directly and measurably during disruptions

Sample User: Ravi, 28 — Swiggy Delivery Partner, Chennai
AttributeDetailZoneTambaram, ChennaiWorking Hours10 AM – 10 PM (10 hrs/day, 6 days/week)Weekly Income₹3,500 – ₹4,200VehicleTwo-wheeler (petrol)DeviceAndroid mid-range, basic UPI literacyKey RisksNortheast monsoon (Oct–Dec), heatwaves (Apr–Jun)
Disruption Scenarios

Scenario 1 — Heavy Rain (T-01)
IMD issues Red Alert for Chennai. Rainfall > 65mm in 3 hours. Ravi cannot ride safely — platform order volume drops 80%. He loses ~₹600 for the day. GigShield auto-credits ₹480 (80% of daily avg) to his UPI within 30 minutes. Zero action needed from Ravi.

Scenario 2 — City-Wide Bandh (T-05)
Unplanned bandh declared in Chennai. Roads blocked, restaurants shut. Zero deliveries possible for 8 hours (weekly loss ≈ ₹700). Cross-referenced News API + Traffic API fires the social trigger automatically. Payout proportional to affected hours.

Scenario 3 — Extreme Heat (T-03)
IMD issues Heatwave alert. Temperature > 43°C, Heat Index > 52°C. Ravi stops working after 2 hours. Heat trigger fires. Payout calculated for estimated lost hours (5 hrs × avg hourly rate).

Scenario 4 — Severe Air Pollution (T-04)
AQI spikes to 380 (Severe) in Ravi's zone. Ravi reduces hours by 60%. AQI trigger fires. Zone-specific payout initiated proportional to coverage hours lost.

Coverage Boundaries
✅ Covered❌ NOT CoveredIncome lost due to rain/flood halting deliveriesVehicle breakdown or repair costsIncome lost due to extreme heat making work unsafeHealth treatment / hospitalisationIncome lost during city-wide bandh / curfewAccident medical billsIncome lost due to severe AQI disruptionLife insurance

💰 Weekly Premium Model
GigShield operates on a weekly subscription pricing model aligned with how gig workers earn and spend.
Workers pay a small weekly premium (auto-debited every Monday via UPI AutoPay / Razorpay Subscriptions). The premium is dynamically adjusted by our AI/ML risk engine based on hyper-local factors.


Historical disruption frequency in the worker's pin-code zone
Worker's average weekly earnings (higher earnings = higher coverage value)
Season/monsoon risk calendar
Zone flood/waterlogging history

→ Full model: Financial model | weekly premium model

⚡ Parametric Triggers
A parametric trigger is an objective, pre-defined threshold tied to real-world data. When crossed, a claim is automatically initiated — no paperwork, no claim officer, no disputes.

🤖 AI / ML Integration Plan

1. Dynamic Premium Calculation

Model: XGBoost regression trained on historical weather, zone, and earnings data
Features: Zone flood history, monsoon calendar, worker earnings tier, historical claim rate per zone
Output: Personalized weekly premium — e.g., ₹2 less per week for workers in zones with low waterlogging history

2. Fraud Detection

Model: Isolation Forest (unsupervised anomaly detection — no labelled fraud data needed)
Signals monitored: GPS location vs. claimed zone, claim frequency patterns, duplicate claim attempts, cross-worker pattern anomalies in same zone
Delivery-specific fraud caught: GPS spoofing, fake weather claims, coordinated simultaneous claims

3. Risk Profiling on Onboarding

Model: Clustering (K-Means) to segment workers into risk buckets at registration
Inputs: Operating zone, working hours, vehicle type, platform, season of joining

4. Predictive Disruption Forecasting

Model: Facebook Prophet for time-series seasonal forecasting
Use: Predict next-week disruption likelihood to pre-alert workers and pre-position reserve funds

→ Full AI/ML plan: AI ML Integration plan | Fraud Detection Architecture

🏗️ Platform Choice — Progressive Web App (PWA)

Decision: Web (PWA) over Native Mobile
FactorReasoningNo app store frictionWorkers can add to home screen directlyWorks on any Android deviceNo iOS/Android split developmentOffline supportService worker caches core screens for low-connectivity zonesFaster iterationSingle codebase for web + mobile-webUPI integrationWorks seamlessly via browser-based Razorpay SDK
→ Full justification: Platform Justification

🔧 Tech Stack

Frontend
LayerTechnologyFrameworkReact.js 18Build ToolVite 5StylingTailwind CSS 3State ManagementZustand 4ChartsRecharts 2Maps / HeatmapsLeaflet.js + react-leafletPWAVite PWA PluginPush NotificationsFirebase Cloud Messaging

Backend
LayerTechnologyRuntimeNode.js 20 LTSFrameworkExpress.js 4ORMSequelize 6DatabasePostgreSQL 14Cache + QueueRedis 7Job SchedulerBull 4 (15-min trigger polling)AuthJWT + OTP (MSG91)

AI / ML Service
ComponentTechnologyML Frameworkscikit-learn + XGBoostTime SeriesFacebook ProphetFraud DetectionIsolation ForestAPI ServerFastAPI (Python 3.10)Model TrackingMLflow

External APIs
IntegrationServiceModeWeatherOpenWeatherMap APILive (free tier)Air QualityOpenAQ APILive (free tier)IMD AlertsIMD RSS FeedLive scrapingTrafficTomTom Traffic APIMockNewsNewsAPIFree tierPaymentRazorpay Test ModeSandboxPushFirebase FCMFree tier

Repository Structure
gigshield/
├── frontend/          → React + Vite + Tailwind PWA
├── backend/           → Node.js + Express + Sequelize
├── ml/                → Python FastAPI + scikit-learn models
└── docker-compose.yml → Spins up all 3 services + PostgreSQL + Redis
→ Full stack details: Tech Stack | System architecture | API Integration

🗺️ Application Workflow

Onboarding — Worker registers with phone number (OTP), selects zone, platform, working hours. AI risk profiler assigns tier suggestion.
Policy Creation — Worker selects weekly plan. UPI AutoPay set up. Policy active from next Monday.
Trigger Monitoring — Every 15 minutes, 5 data sources are polled. Thresholds checked against active worker zones.
Automatic Claim — Threshold breached → fraud validation → claim auto-generated → payout queued.
Instant Payout — UPI transfer within 30 minutes. Worker notified via push notification.
Dashboard — Worker sees weekly coverage status, earnings protected, claim history.

→ Full workflow: Application Workflow

📅 Development Roadmap
PhaseTimelineFocusPhase 1March 4–20Ideation, persona research, architecture design, documentationPhase 2March 21 – April 4Registration, policy management, dynamic premium, claims enginePhase 3April 5–17Advanced fraud detection, payout simulation, analytics dashboard, final pitch
→ Detailed plan: Developemt roadmap

📂 Repository Index

File                                         Description
AI ML Integration Plan            ML models for pricing, risk profiling, fraud detection
API Integration                   External API integrations and data flow
Analytics Dashboard               Dashboard design for workers and admin
Application Workflow              End-to-end user journey and system workflow
setup and installation            Local dev setup instructions
Developemt roadmap                6-week phased development plan
Platform Justification            PWA vs. native mobile decision rationale
Tech Stack                        Full technology choices with justification
System architecture               Full system design and component diagram
Fraud Detection Architecture      Fraud detection layers and signals
Parametric Triggers               5 triggers with thresholds, APIs, and payout logic
Financial model                   Revenue, claims, and sustainability model
weekly premium model              Weekly pricing structure and tier definitions
Persona and scenarios             Detailed user persona (Ravi) and 4 disruption scenarios
