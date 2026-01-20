# Lab M1.04 - Cloud Cost Estimation and Budgets

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-cost-estimation-budgets](https://github.com/cloud-engineering-bootcamp/ce-lab-cost-estimation-budgets)

**Activity Type:** Individual  
**Estimated Time:** 30-45 minutes (core), up to 60 minutes with bonus tasks

## Learning Objectives

- [ ] Use the AWS Pricing Calculator to estimate project costs
- [ ] Configure billing alerts to prevent unexpected charges
- [ ] Analyze cost trade-offs between different service configurations
- [ ] Enable Cost Explorer and review spending patterns
- [ ] Apply cost optimization strategies

## Prerequisites

- [ ] AWS account with billing access
- [ ] Understanding of AWS pricing models
- [ ] Completed previous S3 and EC2 labs (helpful but not required)

---

## Introduction

Cloud costs can spiral out of control quickly if not monitored. In this lab, you'll learn to estimate costs before deploying resources, set up alerts to catch overspending early, and analyze where your money goes.

**Real-world relevance:** Cost management is a core cloud engineering skill. Companies hire "FinOps" engineers specifically to optimize cloud spending.

---

## Your Task

**What you'll create:**
- Cost estimate for a sample web application
- Billing alarm triggered at$10 threshold
- Cost Explorer report showing your current spending
- Document comparing cost scenarios

**Success criteria:**
- [ ] AWS Pricing Calculator estimate completed and saved
- [ ] Billing alarm configured and tested
- [ ] Cost Explorer enabled and explored
- [ ] Screenshots submitted showing all configurations
- [ ] Written analysis of cost optimization opportunities

**Time limit:** 30-45 minutes

---

## Step-by-Step Instructions

### Step 1: Create a Cost Estimate

**Scenario:** You're deploying a simple web application with the following requirements:

- **Web Server:** 1 EC2 t3.medium instance running 24/7
- **Database:** 1 RDS db.t3.micro instance (MySQL)
- **Storage:** 100 GB in S3 Standard
- **Data Transfer:** 500 GB outbound per month
- **Region:** US East (N. Virginia)

**Using AWS Pricing Calculator:**

1. Navigate to [https://calculator.aws](https://calculator.aws/)

2. Click "Create estimate"

3. **Add EC2 Instance:**
   - Search for "EC2"
   - Click "Configure"
   - **Region:** US East (N. Virginia)
   - **Instance type:** t3.medium
   - **Pricing strategy:** On-Demand
   - **Number of instances:** 1
   - **Usage:** 730 hours/month (24/7)
   - **Operating system:** Linux
   - Add to estimate

4. **Add RDS Database:**
   - Search for "RDS"
   - **Database engine:** MySQL
   - **Instance type:** db.t3.micro
   - **Deployment:** Single-AZ
   - **Storage:** 20 GB General Purpose SSD
   - **Usage:** 730 hours/month
   - Add to estimate

5. **Add S3 Storage:**
   - Search for "S3"
   - **Storage class:** S3 Standard
   - **Storage amount:** 100 GB per month
   - **PUT requests:** 10,000 per month
   - **GET requests:** 100,000 per month
   - Add to estimate

6. **Add Data Transfer:**
   - In EC2 configuration, scroll to "Data Transfer"
   - **Outbound data transfer:** 500 GB per month
   - Update estimate

7. **Review Total:**
   - See monthly and 12-month total costs
   - Identify which service costs the most

8. **Save and Share:**
   - Click "Save estimate"
   - Click "Share" → "Generate public link"
   - Copy the link

**Expected outcome:** Total monthly cost estimate around $70-90/month.

---

### Step 2: Compare Cost Scenarios

Now create a second estimate with cost optimizations:

**Scenario 2 (Optimized):**
- **Web Server:** 1 EC2 t3.small (instead of medium) running only business hours (12 hours/day, 5 days/week)
- **Database:** Same as before
- **Storage:** 100 GB in S3 Intelligent-Tiering (instead of Standard)
- **Data Transfer:** Same as before

1. Create a new estimate in the calculator

2. Configure the optimized scenario

3. Compare the two estimates:
   - What's the cost difference?
   - What are the trade-offs?
   - When would each scenario be appropriate?

4. Save this estimate as well

**Document your findings in a text file:** `cost-analysis.txt`

---

### Step 3: Set Up a Billing Alarm

**Enable Billing Alerts:**

1. Sign in to AWS Console (use root user or IAM user with billing permissions)

2. Navigate to: Click your account name (top right) → Billing Dashboard

3. Left sidebar → "Billing preferences"

4. Check ☑ "Receive Billing Alerts"

5. Enter your email address

6. Click "Save preferences"

**Create CloudWatch Billing Alarm:**

1. Navigate to CloudWatch:
   - AWS Console → Search "CloudWatch" → CloudWatch Dashboard

2. Left sidebar → Alarms → Billing

3. Click "Create alarm"

4. Click "Select metric"

5. Choose: Billing → Total Estimated Charge

6. Check ☑ USD

7. Click "Select metric"

8. **Set threshold:**
   - **Whenever EstimatedCharges is:** Greater than
   - **Threshold value:** `10` (USD)

9. Click "Next"

10. **Configure notification:**
    - **Alarm state trigger:** In alarm
    - **SNS topic:** Create new topic
    - **Topic name:** `billing-alerts`
    - **Email:** Your email address
    - Click "Create topic"

11. Click "Next"

12. **Name the alarm:**
    - **Alarm name:** `billing-alert-$10`
    - **Description:** `Alert when estimated charges exceed $10`

13. Click "Next"

14. Review and click "Create alarm"

15. **Confirm SNS subscription:**
    - Check your email
    - Click the confirmation link

**Expected outcome:** You'll receive an email if your estimated monthly bill exceeds $10.

**Take a screenshot** of your alarm configuration.

---

### Step 4: Enable and Explore Cost Explorer

**Enable Cost Explorer:**

1. Billing Dashboard → Cost Explorer

2. If not enabled, click "Enable Cost Explorer"
   - Note: May take up to 24 hours to populate data

3. If already enabled, click "Launch Cost Explorer"

**Explore Your Costs:**

1. **Monthly costs:**
   - View last 3 months of spending
   - Identify trends

2. **Cost by service:**
   - Group by: Service
   - See which services cost the most

3. **Daily costs:**
   - Change granularity to "Daily"
   - Identify any spikes

4. **Forecast:**
   - Enable "Forecast"
   - See predicted costs for next month

**Take screenshots** of:
- Cost by service (pie chart or bar chart)
- Daily cost trend
- Forecasted costs

---

### Step 5: Analyze and Document

Create a document `SOLUTION.md` with:

**1. Cost Estimates:**
- Link to Scenario 1 (baseline) estimate
- Link to Scenario 2 (optimized) estimate
- Comparison table showing cost differences

**2. Screenshots:**
- Pricing Calculator estimate (both scenarios)
- Billing alarm configuration
- Cost Explorer views

**3. Analysis:**
Answer these questions:

- **What service is the most expensive in Scenario 1?**
- **How much money did you save in Scenario 2? What percentage savings?**
- **What are the trade-offs of running the EC2 instance only during business hours?**
- **If your website has unpredictable traffic, which pricing model would you use and why?**
- **How would you further optimize costs without impacting performance?**

---

## Submission

Submit the following to the student portal:

1. **AWS Pricing Calculator Links:**
   - Scenario 1 (baseline) public link
   - Scenario 2 (optimized) public link

2. **Screenshots:**
   - `billing-alarm-config.png`
   - `cost-explorer-by-service.png`
   - `cost-forecast.png`

3. **Analysis Document:** `SOLUTION.md` (or PDF)

---

## Verification Checklist

- [ ] Two cost estimates created and saved
- [ ] Billing alarm configured for $10 threshold
- [ ] SNS subscription confirmed (check email)
- [ ] Cost Explorer enabled and explored
- [ ] All required screenshots taken
- [ ] Analysis questions answered thoroughly
- [ ] Links and files submitted

---

## Bonus Challenges

### Bonus 1: Create Multiple Billing Alarms

Set up tiered alarms:
- $10 threshold (early warning)
- $50 threshold (take action)
- $100 threshold (emergency)

### Bonus 2: Tag Resources and Analyze Costs by Tag

1. Tag your S3 buckets with `Project: Bootcamp`
2. Enable cost allocation tags in Billing preferences
3. Wait 24 hours
4. View costs grouped by tag in Cost Explorer

### Bonus 3: Estimate Costs for a Real Project

Choose a project you want to build and estimate its monthly costs:
- What services will you use?
- How much traffic do you expect?
- How can you optimize costs?

### Bonus 4: Set Up a Budget

1. Billing → Budgets → Create budget
2. Choose "Cost budget"
3. Set monthly limit (e.g., $25)
4. Configure alerts at 50%, 80%, 100% of budget
5. Create budget

---

## Troubleshooting

### Can't access Billing Dashboard

**Cause:** IAM user doesn't have billing permissions

**Solution:**
1. Sign in as root user
2. Or ask account owner to grant you billing permissions:
   - IAM → Users → Your user → Add permissions → Attach policy: `Billing`

### Cost Explorer shows no data

**Cause:** Cost Explorer was just enabled or account has no charges yet

**Solution:**
- Wait 24 hours after enabling
- If account is brand new, deploy some resources first (free tier resources won't generate costs)

### Email confirmation not received

**Cause:** Email in spam or wrong email address

**Solution:**
- Check spam folder
- Check SNS subscription in CloudWatch alarm configuration
- Resend confirmation or update email address

---

## Hints

<details>
<summary><strong>Hint 1:</strong> I can't find the Billing Dashboard</summary>

1. Click your account name in the top-right corner
2. Choose "Billing Dashboard" from the dropdown
3. If you don't see it, you may need billing permissions (see Troubleshooting)

</details>

<details>
<summary><strong>Hint 2:</strong> How do I calculate hourly costs?</summary>

For services charged by the hour:
- 24/7 usage = 730 hours/month (24 hours × 365 days ÷ 12 months)
- Business hours only (12 hrs/day, 5 days/week) = ~260 hours/month

Example:
- t3.medium on-demand = $0.0416/hour
- 24/7 = $0.0416 × 730 = $30.37/month
- Business hours = $0.0416 × 260 = $10.82/month

</details>

<details>
<summary><strong>Hint 3:</strong> Which services typically cost the most?</summary>

For most workloads:
1. **Compute (EC2, RDS):** Usually 50-70% of costs
2. **Data Transfer:** Can be surprisingly expensive
3. **Storage (S3, EBS):** Moderate but adds up at scale

</details>

---

## AI Usage Guidelines

**Allowed:**
- ✅ Ask AI to explain pricing concepts
- ✅ Ask AI for cost optimization strategies
- ✅ Ask AI to help calculate costs

**Recommended:**
- Use the calculator yourself first
- Ask AI: "What are common cost optimization strategies for EC2?"
- Verify AI recommendations with AWS documentation

---

## Learning Reflection

1. **What surprised you most about AWS pricing?**
2. **How would you explain "pay-as-you-go" to a non-technical person?**
3. **What strategies would you use to prevent a surprise $1,000 bill?**
4. **How does cloud pricing compare to buying your own servers?**

---

## Additional Resources

- [AWS Pricing Calculator User Guide](https://docs.aws.amazon.com/pricing-calculator/)
- [AWS Cost Optimization Best Practices](https://aws.amazon.com/architecture/cost-optimization/)
- [AWS Billing and Cost Management](https://docs.aws.amazon.com/account-billing/)

---

**Good luck! 💰**
