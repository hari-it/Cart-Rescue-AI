
# CartRescue AI
Real-Time Cart Abandonment Prediction & Intelligent Recovery Platform
CartRescue AI is an AI-powered e-commerce solution that predicts when a customer is likely to abandon their shopping cart, identifies the possible reason behind the risk, and recommends a suitable recovery action.
Instead of giving the same discount to every customer, CartRescue AI combines customer session behavior, cart activity, payment signals, machine learning, and business rules to decide when to intervene, what action to take, and when to do nothing.
> Predict the risk. Understand the reason. Take the right action. Protect the margin.

# Table of Contents
Problem Statement
Why Cart Abandonment Happens
Our Solution
Project Objectives
Complete Workflow
Dataset
Data Processing
Feature Engineering
Machine Learning
Model Evaluation
Risk Scoring
Abandonment Diagnosis
Intervention Engine
Margin Protection & Guardrails
Real-Time Rescue Experience
Store Simulator
Merchant Command Dashboard
Model Diagnostics
Strategy Rules
Holdout Experiment
Business Impact
System Architecture
Technology Stack
API
Project Structure
Project Deliverables
Expected Outcomes
Getting Started
Demo
Future Scope
Team
License

# Problem Statement
Cart abandonment is a major challenge in e-commerce. A customer may browse products, add an item to the cart, and even start checkout, but still leave without completing the purchase.
The reason is not always the same.
A customer might be facing a payment problem, comparing prices with another platform, hesitating because of shipping charges, or simply experiencing friction during checkout.
Traditional cart-recovery systems often respond with the same generic discount or message to every customer. This can lead to unnecessary discounts and does not address the actual reason behind abandonment.
The core problem
We need a system that can:
Identify customers who are likely to abandon their carts.
Understand the possible reason behind the risk.
Decide whether an intervention is actually needed.
Recommend one suitable recovery action.
Keep the action within merchant-defined margin limits.
Measure whether the intervention actually improves recovery.

# Why Cart Abandonment Happens
CartRescue AI considers several common situations that can contribute to abandonment:
Unexpected shipping costs
UPI / Net Banking payment failure
Unfavorable delivery dates
Comparing prices on other apps
Lack of Cash on Delivery (COD) option
Friction in the checkout form
Extended browsing or hesitation
Other session-level behavioral signals
The important point is that different problems may require different solutions.
For example, a payment failure should not automatically result in a discount.

# Our Solution
CartRescue AI turns cart abandonment prediction into an actionable recovery workflow.
text
Customer Browses
       ↓
Adds Product to Cart
       ↓
Session & Cart Signals
       ↓
Abandonment Risk Prediction
       ↓
Risk + Reason Diagnosis
       ↓
Choose One Action
       ↓
Business & Margin Guardrails
       ↓
Real-Time Intervention
       ↓
Measure Recovery & ROI

The system is designed around a simple principle:
> Do not discount blindly. Understand the customer first.
A low-risk customer may receive no intervention, while a high-risk customer with a payment issue may receive payment assistance instead of a discount.

# Project Objectives
1. Predict Cart Abandonment
Estimate the probability that an active cart session will end without a purchase.
2. Diagnose Risk
Use session and event signals to understand the behavior associated with the predicted risk.
3. Recommend One Action
Select one suitable intervention for the session. Do Nothing is also a valid action.
4. Protect Merchant Margins
Keep discounts and incentives within predefined business limits.
5. Validate Recovery
Use control and treatment groups to estimate whether interventions create incremental recovery.
6. Provide Merchant Visibility
Give merchants a dashboard for monitoring risk, interventions, recovery performance, and financial impact.

# Complete Workflow
                E-Commerce Session
                        │
                        ▼
              Event & Cart Data
                        │
                        ▼
              Data Processing
                        │
                        ▼
              Feature Engineering
                        │
                        ▼
              ML Risk Prediction
                        │
                        ▼
              Risk Classification
                        │
                        ▼
              Reason / Signal Analysis
                        │
                        ▼
             Intervention Engine
                        │
                        ▼
             Guardrail Validation
                        │
                ┌───────┴───────┐
                ▼               ▼
          Customer Action   Do Nothing
                │
                ▼
          Recovery Tracking
                │
                ▼
             ROI Analysis


# Dataset
The project uses e-commerce session and event data containing browsing, cart, checkout, payment, and purchase activity.
Dataset Summary
Metric	Count
Total Sessions	120,000
Total Events	760,958
Sessions with Add-to-Cart	81,518
Sessions with Checkout	44,909
Sessions with Purchase	33,580
Abandoned Cart Sessions	47,938
Event Types
text
page_view
add_to_cart
checkout
purchase

Cart Funnel
text
120,000 Total Sessions
        │
        ▼
81,518 Add-to-Cart Sessions
        │
        ▼
44,909 Checkout Sessions
        │
        ▼
33,580 Purchase Sessions

Cart Outcomes
Outcome	Sessions	Percentage
Abandoned	47,938	58.81%
Purchased	33,580	41.19%
Total Cart Sessions	81,518	100%

# Data Processing
The raw event data is converted into a session-level dataset suitable for machine learning.
The processing pipeline includes:
Loading session and event data.
Inspecting event types and data quality.
Handling event-level missing values according to their meaning.
Converting timestamps into usable datetime values.
Grouping events by session.
Identifying cart-active sessions.
Identifying sessions that completed a purchase.
Creating the abandonment target.
Generating session-level behavioral features.
Preparing the final ML dataset.
Target Definition
For cart-active sessions:
text
Purchased = 1
Abandoned = 0

The project uses the cart session outcome to train the abandonment prediction model.

# Feature Engineering
Raw events are transformed into session-level features that describe the customer's shopping behavior.
Important features include:
`avg_dwell_time_sec`
`has_checkout`
`cart_value_usd`
`num_page_views`
`device_mobile`
Payment-related signals
Cart activity
Browsing behavior
Traffic source
Example:
text
page_view
page_view
add_to_cart
checkout

becomes session-level information such as:
text
Number of page views
Checkout started
Cart value
Time spent browsing
Device type


# Machine Learning
text
Raw Data
   ↓
Data Cleaning
   ↓
Session Aggregation
   ↓
Feature Engineering
   ↓
Target Creation
   ↓
Train/Test Preparation
   ↓
Model Training
   ↓
Model Evaluation
   ↓
Model Selection
   ↓
Risk Prediction




# Top Predictive Signals
The current model evaluation identifies these among the strongest predictive features:
`avg_dwell_time_sec` — browsing hesitation
`has_checkout` — checkout intent
`cart_value_usd` — cart value
`num_page_views` — repeated browsing
`device_mobile` — device behavior

# Risk Scoring
Each cart-active session receives an abandonment probability and is classified into:
text
LOW
MEDIUM
HIGH

Example:
text
Session
   ↓
Abandonment Probability: 82%
   ↓
Risk Level: HIGH
   ↓
Reason / Signal Analysis
   ↓
Intervention Recommendation


# Abandonment Diagnosis
Prediction alone is not enough. CartRescue AI also uses behavioral and session signals to provide context for the predicted risk.
Payment Failure
text
Payment Attempt
      ↓
Payment Failure
      ↓
High Risk
      ↓
Payment Assistance

Price Comparison / Hesitation
text
Repeated Browsing
      ↓
High Product Interest
      ↓
Possible Price Friction
      ↓
Targeted Intervention

Checkout Friction
text
Checkout Started
      ↓
Extended Hesitation
      ↓
Possible Checkout Friction
      ↓
Checkout Assistance

Low Risk
text
Low Abandonment Probability
      ↓
Do Nothing


# Intervention Engine
Possible actions include:
Situation	Possible Action
Low risk	Do Nothing
Checkout hesitation	Checkout assistance
Payment issue	Payment recovery/help
Shipping concern	Free shipping
Price sensitivity	Targeted discount
High-value/high-risk session	Controlled incentive
General hesitation	Reminder / urgency message
The system is designed to recommend one clear action per session.

# Margin Protection & Guardrails
The intervention engine applies business rules before generating an offer.
text
Prediction
    ↓
Decision
    ↓
Business Rules
    ↓
Final Action

Example:
text
Predicted Risk = HIGH
        ↓
Potential Discount = 20%
        ↓
Merchant Maximum = 15%
        ↓
Final Allowed Discount = 15%

Guardrails can include:
Maximum discount percentage
Cart-value thresholds
Risk thresholds
Campaign limits
Allowed intervention types
Customer consent/channel requirements
The objective is to maximize incremental recovery, not simply maximize discounts.

# Real-Time Rescue Experience
text
Customer Activity
       ↓
Risk Becomes High
       ↓
Rescue Trigger
       ↓
Personalized Message
       ↓
Recommended Offer
       ↓
Countdown / Urgency
       ↓
Customer Action

The current application includes a dynamic rescue offer experience with a 10-minute countdown timer.

# Interactive Store Simulator
The project includes an interactive e-commerce store simulator for testing customer scenarios.
Features
Product catalog
Shopping cart
Customer session simulation
Session configuration
Preset test scenarios
Real-time risk gauge
AI risk prediction
Intervention recommendations
Dynamic rescue popup
Countdown timer

# Merchant Command Dashboard
The merchant dashboard provides:
Business Metrics
Total cart sessions
Abandonment rate
Purchase rate
Recovery performance
Recovered revenue
ROI
AI Metrics
Risk distribution
Predicted abandonment probability
High-risk sessions
Model performance
Feature importance
Operational Information
Session telemetry
Intervention activity
Active strategy rules
Recommended actions

# Model Diagnostics
The Model Diagnostics section provides visibility into:
Model comparison
ROC-AUC
F1-score
Recall
Precision
Feature importance
Risk distribution
Prediction behavior

# Strategy Rules
Strategy Rules control how interventions are generated.
Examples include:
Risk thresholds
Maximum discount
Cart-value conditions
Urgency settings
Intervention preferences
Campaign restrictions
text
ML Model
   ↓
Risk Score
   ↓
Strategy Rules
   ↓
Guardrails
   ↓
Final Intervention


# Business Impact
Based on the current dataset and simulation results:
Metric	Result
Cart-Active Sessions	81,518
Abandoned Carts	47,938
Abandonment Rate	58.81%
Potential Lost Revenue	$5.39M
Simulated Recovered Carts	13,422
Simulated Recovery Lift	+28.4%
Net Recovered Revenue	$1,358,977.50
Estimated ROI Multiple	6.4x
These figures represent the current project simulation and demonstrate the potential business impact of targeted cart recovery. They are not guaranteed production results.

# System Architecture

                         ┌───────────────────────┐
                         │  E-Commerce Activity  │
                         │ Sessions / Events     │
                         │ Cart / Payment        │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │ Data Processing &     │
                         │ Feature Engineering   │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │ ML Risk Prediction    │
                         │ HistGradientBoosting  │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │ Risk + Diagnosis      │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │ Intervention Engine   │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │ Business Guardrails   │
                         │ & Strategy Rules      │
                         └───────────┬───────────┘
                                     │
                        ┌────────────┴────────────┐
                        ▼                         ▼
              ┌──────────────────┐     ┌──────────────────┐
              │ Customer Rescue  │     │ Merchant         │
              │ Experience       │     │ Dashboard        │
              └──────────────────┘     └──────────────────┘
                        │                         │
                        └────────────┬────────────┘
                                     ▼
                            Recovery & ROI


# Technology Stack
Machine Learning & Data
Python
Pandas
NumPy
Scikit-learn
Joblib
Backend
Flask
Flask-CORS
Frontend
HTML5
CSS3
JavaScript
Glassmorphism UI
Visualization
Chart.js
FontAwesome 6

# REST API
`POST /api/predict`
Predicts abandonment risk for a shopping session.
Example Request
json
{
  "events": [
    {
      "event_type": "page_view",
      "timestamp": "2026-08-08 10:00:00"
    },
    {
      "event_type": "add_to_cart",
      "timestamp": "2026-08-08 10:03:00",
      "qty": 1,
      "price_usd": 199.99,
      "category": "Electronics"
    }
  ],
  "customer": {
    "age": 28,
    "marketing_opt_in": 1
  },
  "device": "mobile",
  "source": "paid"
}

Example Response
json
{
  "abandonment_probability": 0.9999,
  "risk_tier": "HIGH",
  "model_used": "HistGradientBoosting"
}

`POST /api/rescue`
Generates a recovery recommendation using:
Abandonment risk
Session context
Cart information
Strategy rules
Merchant margin limits
Intervention guardrails

# Project Structure
text
Cart_Rescue_AI/
│
├── ml/
│   ├── clean_data.py
│   ├── eda.py
│   ├── features.py
│   ├── train_models.py
│   └── intervention.py
│
├── models/
│   └── cart_abandonment_model.joblib
│
├── reports/
│   ├── eda_summary_report.json
│   └── model_evaluation_metrics.json
│
├── static/
│   ├── index.html
│   ├── styles.css
│   └── app.js
│
├── app.py
├── cart_rescue_standalone.html
└── README.md


# Project Deliverables
The project is designed to deliver:
> Working MVP
A complete flow from customer session activity to risk prediction and recovery recommendation.
> Machine Learning Model
A trained abandonment prediction model with model comparison and evaluation.
> Risk Scoring
Session-level abandonment probability and risk classification.
> Abandonment Diagnosis
Behavioral signals that help explain why a session may be at risk.
> Intervention Engine
A policy-bounded system that recommends one suitable action.
> Margin Protection
Business rules that prevent uncontrolled discounting.
> Store Simulator
An interactive environment for demonstrating customer scenarios.
> Merchant Dashboard
Monitoring of customer risk, interventions, and business metrics.
> Model Diagnostics
Model performance and feature-level analysis.
> Experiment Framework
Control/treatment evaluation for measuring incremental recovery.
> REST API
Prediction and rescue endpoints.
> Standalone Demo
A single-file browser version for easy demonstration.
> Technical Documentation
Architecture, ML workflow, setup instructions, and implementation details.

# Expected Outcomes
The final system demonstrates that cart abandonment prediction can be converted into an actionable business workflow:
text
Predict
   ↓
Understand
   ↓
Decide
   ↓
Intervene
   ↓
Measure

The intended outcomes are:
Identify customers at risk of abandoning.
Explain important signals behind the risk.
Distinguish different abandonment situations where the available data supports it.
Recommend one bounded action.
Allow the system to choose Do Nothing.
Protect merchant margins.
Evaluate intervention effectiveness.
Provide merchant-level visibility.
Demonstrate measurable business impact.

# Responsible AI & Business Guardrails
Margin Protection
Discounts remain within merchant-defined limits.
Explainability
Important signals contributing to risk are exposed.
Auditability
The system can track:
Session
Risk score
Risk level
Risk signals
Recommended action
Applied intervention
Consent & Communication
Any future integration with email, SMS, WhatsApp, or push notifications should respect user consent and applicable communication requirements.
Controlled Incentives
The system should not automatically issue unlimited or unnecessary discounts.

# Demo Flow

1. Open Store Simulator
        ↓
2. Select a customer scenario
        ↓
3. Add a product to the cart
        ↓
4. Observe session behavior
        ↓
5. Generate abandonment risk
        ↓
6. View risk level and signals
        ↓
7. View recommended intervention
        ↓
8. Trigger rescue experience
        ↓
9. Open Merchant Command
        ↓
10. Review business and AI metrics

# Future Scope
Possible future improvements include:
Real-time event streaming
Live e-commerce platform integration
Payment gateway integration
Email/SMS/WhatsApp recovery campaigns
CRM integration
Real A/B testing
Customer Lifetime Value integration
Uplift modeling
Continuous model monitoring
Probability calibration
Out-of-time validation
Production cloud deployment
Real-time feature stores
More advanced agent-based decision making

# What Makes CartRescue AI Different?
A traditional recovery system may work like this:

Customer Abandons
       ↓
Send Generic Discount

# CartRescue AI aims to work like this:

Customer Behavior
       ↓
Predict Abandonment Risk
       ↓
Understand Possible Reason
       ↓
Select One Action
       ↓
Check Business Rules
       ↓
Intervene Only When Useful
       ↓
Measure Incremental Recovery

The project therefore goes beyond:
>"Will this customer abandon the cart?"**
It asks:
> "Is this customer likely to abandon, why might they be at risk, what is the best action, and is that action worth the cost?"**
