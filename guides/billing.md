# How Billing Works

The following applies to accounts created via Rollbar.com.  See the section <a href="#partner-billing">Partner Billing</a> for details on how billing works if you created an account elsewhere.
{: .info}

## Billing Cycles

For both monthly and annual plans, your account will have a billing cycle that starts on the day of the month when you originally signed up for the plan.  The billing cycle is used to calculate your monthly usage.   If you sign up after the 28th then your billing cycle date will vary depending on the length of the month.

## On Demand Events & Upgrades
The following applies to monthly subscriptions for accounts created via Rollbar.com.  Annual plans are not automatically upgraded.
{: .info}

If you exceed your monthly event limit, you can now pay *per event* over the limit.  If your on demand charge is sufficiently high that it would be more economical to upgrade to the next plan, then we'll do it for you automatically and you won't be charged for the overages.  Here's how it works:

| Plan	| Monthly Cost	| Events/ Month	| Cost per 1,000 events over limit	| *We'll automatically upgrade you if your on demand usage reaches...* |
|-------|----------------|---------------|-----------------------------------|----------|
| Bootstrap |	$49	| 100,000 |	$1.00	| 100,000 events ($100.00) |
| Startup | $149	| 500,000	| $0.60 | 250,000 events ($150.00) |
| Growth	| $299	| 1,500,000 |	$0.40 |	750,000 events ($300.00) |
| Premium	| $599	| 4,000,000 |	$0.30 |	N/A |
				
Once your account has been automatically upgraded, it will remain at the new plan level for future billing cycles.  You can change your plan at any time by going to **Account Settings --> Choose Plan**.  If you choose a lower plan level, the change will take effect at the start of your next monthly billing cycle.

You may also upgrade your subscription manually at any time by going to **Account Settings --> Choose Plan**.

### Disabling On Demand

If you are on a strict budget and don't mind missing some errors, then you can choose to disable on demand events at **Account Settings --> Billing Info**.  If on demand is disabled and you reach your plan limit, we will not process new errors until your next billing cycle begins.

### On Demand Billing
On demand event charges are calculated at the end of your billing cycle, and are included in the next month's subscription charge.

Here's an example of how this works:

```
Your bootstrap ($49/mo) plan is billed each month on the 10th.

During the period April 10 - May 9, you use 109,532 events (9,532 over your monthly limit).

On May 10th, your monthly charge will be $58.53
* $9.53 for on demand events during April 10 - May 9.
* $49.00 for your subscription May 10 - June 9.
```

### Upgrade Billing
If your account is upgraded (manually by you or automatically by us), then you will be charged immediately for the difference between your old plan and your new one.  Your monthly billing date will remain the same.

Here's an example of how this works:

```
Your bootstrap ($49/mo) plan is billed each month on the 10th.

On the April 20, you choose to upgrade to the Startup ($149/mo) plan, or your on demand usage exceeds 100,000 events.

You are immediately charged ($149 - $49 = $100) for the upgrade to Startup.

Your next charge will be on May 10 for $149.
```

## Annual Plans

Rollbar annual plans offer a way to pre-pay for usage at a rate equivalent to receiving two months free in a year.

### On Demand & Annual Plans

If you are on an annual plan and exceed your monthly event limit, the cost of the additional events is deducted from the remaining balance of your prepayment, and your annual plan will end before 12 months.

When the funds in an annual plan are fully depleted, your account will be charged the amount of the annual plan again, and a new annual cycle will begin.

## Partner Billing

### Heroku

If you created your account through Heroku, then your Rollbar subscription is included in your monthly Heroku bill.

Rollbar cannot automatically upgrade accounts created through Heroku.  If you reach your monthly event limit, then error data will not be processed until you migrate your plan ([instructions here](https://devcenter.heroku.com/articles/rollbar#migrating-between-plans)) or a new monthly billing cycle begins.

