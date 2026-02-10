# Lab 01 – AWS WAFv2 Basics: Web ACL Design and Association

## Threat Context
Applications exposed through ALBs or CloudFront are common targets for
layer 7 attacks such as injection attempts, malicious scanners, and abuse
of public endpoints.

Without a Web Application Firewall, these requests reach the application
layer uninspected, increasing both security risk and operational noise.

## Objective
Create and associate an AWS WAFv2 Web ACL to an application entry point
and understand how AWS WAF evaluates traffic.

The focus of this lab is **correct WAF attachment and rule evaluation order** —
not just creating a Web ACL.

## What I Built
- AWS WAFv2 Web ACL
- Associated Web ACL with an Application Load Balancer
- Configured default action and rule priority
- Verified request flow through the WAF

## Why Association Matters
A Web ACL provides **zero protection** unless it is correctly associated.

In AWS, WAF behavior differs depending on scope:
- **ALB / API Gateway (Regional)**
- **CloudFront (Global)**

Choosing the wrong scope or missing the association step results in
a false sense of security — the WAF exists, but traffic bypasses it.

## Rule Evaluation Order
AWS WAF evaluates rules **top to bottom**, stopping at the first matching rule.

This means:
- High-priority allow rules can override protections
- Poor ordering can weaken otherwise strong rule sets
- Testing rule behavior is critical before enforcement

Misordered rules are a common production failure mode.

## Validation
- Confirmed Web ACL association with ALB
- Generated test requests to ensure traffic was inspected
- Verified rule evaluation using WAF metrics

## Tradeoffs and Limitations
- This lab does not include managed rule groups yet
- No logging enabled at this stage
- No false positive tuning performed

Those gaps are intentional and addressed in later labs.

## Production Considerations
In a real environment, I would:
- Enable WAF logging immediately
- Start new rules in COUNT mode
- Use metrics to baseline normal traffic
- Introduce managed rules incrementally
- Separate WAFs by environment (dev / staging / prod)

Correct attachment and evaluation logic are foundational.
Everything else builds on this.
