# cloud for enterprises: how to pick the right model, what real plans cost, and where cloud bills quietly spiral

Somebody searching "cloud for enterprises" is usually sitting on one of two problems. Either the company is moving serious workloads off on-premises hardware for the first time, or it's already paying a hyperscaler and has started asking uncomfortable questions about the invoice. Both groups need the same things: a clear picture of the deployment models, an honest look at where the money goes, and actual plan prices instead of "contact sales for a quote."

This article covers all three, and then uses one specific provider — Sharktech, an OpenStack-based cloud host operating since 2003 — as a worked example, with its full current plan lineup, verified pricing, and the independent reviews worth knowing about before you commit.

## What "cloud for enterprises" actually covers

Enterprise cloud isn't one product. It's a set of decisions stacked on top of each other, and conflating them is how projects end up over budget.

**Deployment model.** Public cloud means your workloads run on shared infrastructure managed by a provider — multi-tenant, elastic, metered. Private cloud keeps the infrastructure dedicated to one organization, whether hosted on-site or in a provider's facility, which buys control and compliance headroom at a higher base cost. Hybrid mixes the two, keeping regulated or latency-sensitive systems close to home while bursting everything else into a shared environment.

**Service layer.** IaaS gives you raw compute, storage, and networking — you build and run everything above the hypervisor. PaaS adds managed runtimes and tooling. SaaS is finished software you simply rent. Most enterprises making an infrastructure decision are choosing at the IaaS layer, so that's where this article stays.

**Provider size.** AWS, Azure, and Google Cloud dominate the conversation, but they're not the whole market. Mid-size providers running open-source stacks (typically OpenStack) compete on price transparency, simpler billing, and support you can actually reach by phone. For a lot of enterprises — especially mid-market ones without a dedicated FinOps team — that difference matters more than having 200+ proprietary services available.

## What an enterprise actually needs from a cloud

Before comparing vendors, it helps to write down the requirements that separate an enterprise deployment from a hobby project:

- **Security and compliance.** DDoS mitigation, firewalling at the network layer, private networking between VMs, role-based access, and audit visibility. If you're in a regulated industry, data location and sovereignty rules may narrow your options immediately.
- **Predictable spend.** Hyperscaler billing is famously complex — dozens of line items, regional price differences, and egress fees that punish you for moving your own data. Finance teams care about this more than engineering teams do.
- **An exit strategy.** Vendor lock-in is a real cost. Proprietary managed services are fast to adopt and expensive to leave. Open standards and the ability to export your own disk images change the negotiation entirely.
- **Scalability without re-architecture.** The ability to add CPU, RAM, or storage live, and to distribute a resource pool across many VMs rather than buying rigid presets.
- **Support that answers.** When a production system degrades at 2 a.m., a chatbot funnel is not a strategy. Enterprise buyers consistently weight phone-accessible, 24/7 human support heavily.
- **Geography.** Data centers close to your users or inside your legal jurisdiction.

None of that is exotic. What varies wildly between providers is how each item is priced and how honestly it's disclosed.

## Where enterprise cloud budgets go wrong

The horror stories are consistent enough to be predictable.

**Egress fees.** Moving data *into* a cloud is usually free. Moving it *out* is not, and outbound transfer can quietly become one of the largest line items on a monthly bill. Worse, high egress pricing acts as a soft lock-in: it makes migration and multi-cloud strategies financially painful, which is exactly the point.

**Billing complexity.** Reserved instances, savings plans, spot pricing, per-region multipliers, and metered services that interact with each other. Large orgs hire people specifically to manage this. Smaller enterprises just overpay.

**Idle and orphaned resources.** Forgotten test VMs, unattached volumes, and over-provisioned instances that nobody decommissions. Every provider suffers from this; the ones with simple per-resource pricing at least make the waste visible.

**Proprietary gravity.** Every managed service you adopt that has no open-standard equivalent raises your switching cost. Six months later, "we should compare providers" turns into a rewrite project.

This is the context in which providers like Sharktech make their pitch: flat, published rates, free inbound transfer, cheap egress, and an OpenStack foundation that keeps the door open. Whether that pitch holds up depends on the details, so let's look at them.

## A worked example: Sharktech's OpenStack cloud

Sharktech has been around since 2003 — it was built largely as a DDoS-protection-focused host, which explains why mitigation is baked into the network rather than sold as an add-on. It runs five data centers: Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam.

The cloud platform is OpenStack-based (delivered through Virtuozzo Hybrid Infrastructure), hyper-converged, with resources spread across multiple servers and storage nodes so a single hardware failure doesn't take your VMs down. A few specifics worth knowing:

- **Multi-tier storage.** You allocate across NVMe, SSD, and HDD within the same environment. Per Sharktech's published estimates: SSD runs around 350 MB/s and 6,000 IOPS per volume, NVMe around 1.2 GB/s and 18,000 IOPS, HDD around 120 MB/s and 3,000 IOPS. NVMe for databases and hot paths, HDD for archives, SSD for everything in between.
- **Networking included.** Private networks, security groups, virtual routers with NAT, floating IPs, load balancing, IPv6, and an integrated VPN for bridging cloud VMs to on-premises infrastructure — the VPN is free of charge.
- **Kubernetes and APIs.** Every public cloud tier ships with security policies, load balancing, network management, routing, and Kubernetes support included at no extra cost. The platform exposes the standard OpenStack REST APIs (Nova for compute, Cinder and Swift for storage, Neutron for networking, Keystone for identity), so Terraform-style automation works without proprietary SDKs.
- **No lock-in mechanics.** You can upload your own ISOs and qcow images and download your disk images whenever you want — for backup, disaster recovery, or a clean exit to another provider.
- **DDoS protection is built in.** The network includes mitigation as standard; third-party reviews consistently note that 60 Gbps of protection comes with plans by default rather than as a paid tier.

The company claims its pricing saves customers "at least 40%" versus hyperscalers, with marketing materials citing 50–80% depending on workload. Treat those as claims, but the structural argument — flat rates, free ingress, egress at $0.002/GB or less — is checkable, and it's the pricing structure itself that does the work.

### How billing works: two models, same infrastructure

Sharktech splits its cloud into Public Cloud and Dedicated Cloud, and the difference is purely financial — the infrastructure and feature set are the same.

**Public Cloud** is pay-as-you-go with a twist that's friendlier than most: each plan includes a fixed resource commit for a fixed monthly price, and you can burst beyond it at published hourly rates. Plans below Enterprise carry a maximum resource cap so a runaway process can't produce a runaway invoice.

The formula, from Sharktech's own documentation:

$$\text{Monthly fee} = \text{Included resources} \times \text{fixed fee} + \text{extra usage} \times \text{hourly rate}$$

**Dedicated Cloud** is the prepaid version: you order a fixed allocation, you get exactly that allocation, and the invoice never moves unless you change the plan. Billing cycles run monthly, quarterly, semi-annually, or annually, with discounts on the longer terms.

### The full plan lineup

Here is every plan currently published on Sharktech's order pages (Los Angeles region shown; Las Vegas, Denver, Chicago, and Amsterdam carry the same tiers). All prices in USD.

| Plan | vCPU (included – max) | RAM (included – max) | SSD storage | Other storage | Bandwidth | Starting price | Billing | Purchase |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Public Cloud – Small** | 4 – 16 | 8 GB – 32 GB | 300 GB – 2,400 GB | HDD up to 4,800 GB; NVMe up to 1,200 GB | 20 TB included, unlimited in | $39.00/mo | Monthly, PAYG overage | [ Get the Small plan](https://portal.sharktech.net/aff.php?aff=1611&pid=602) |
| **Public Cloud – Medium** | 8 – 32 | 16 GB – 64 GB | 800 GB – 6,400 GB | HDD up to 12,800 GB; NVMe up to 3,200 GB | 20 TB included, unlimited in | $79.00/mo | Monthly, PAYG overage | [ Get the Medium plan](https://portal.sharktech.net/aff.php?aff=1611&pid=603) |
| **Public Cloud – Large** | 32 – 128 | 64 GB – 256 GB | 1,500 GB – 12,000 GB | HDD up to 24,000 GB; NVMe up to 6,000 GB | 20 TB included, unlimited in | $249.00/mo | Monthly, PAYG overage | [ Get the Large plan](https://portal.sharktech.net/aff.php?aff=1611&pid=604) |
| **Public Cloud – Enterprise** | 64 – no cap | 128 GB – no cap | 5,000 GB – no cap | HDD and NVMe uncapped | 20 TB included, unlimited in | $499.00/mo (~$0.741/hr) | Monthly, PAYG at discounted rates | [ Get the Enterprise plan](https://portal.sharktech.net/aff.php?aff=1611&pid=605) |
| **Dedicated Cloud** | 8 – 512 | 16 GB – 1,024 GB | Configurable SSD/HDD/NVMe tiers | — | 5 – 300 TB configurable | $86.23/mo | Fixed monthly; discounts quarterly/annual | [ Configure Dedicated Cloud](https://portal.sharktech.net/aff.php?aff=1611&gid=102) |
| **Custom** | Any | Any | Any | Any | Any | Quoted | Quoted | [ Talk to sales about a custom build](https://bit.ly/SharKTech) |

A few numbers behind the table:

- **PAYG overage rates (Small through Large):** CPU $0.0025/hr per core, RAM $0.0035/hr per GB, SSD $0.00006/hr per GB, HDD $0.00002/hr per GB, NVMe $0.00009/hr per GB. Extra public IPv4 addresses cost $1.50/mo each — the first one is free. Bandwidth beyond the included 20 TB bills at $0.002/GB outbound; inbound is unlimited and free.
- **Enterprise gets cheaper overage:** CPU $0.002/hr, RAM $0.003/hr, SSD $0.000045/hr, and bandwidth overage at $0.0015/GB. It's the only public tier with no resource cap, so the discounted rates matter if you're bursting regularly.
- **Every tier includes** security policies, load balancing, network management, routing, and Kubernetes at no extra charge.

If you want to see the full tier configurator with live cost calculation per location, 👉 open the public cloud order pages here and plug in your actual workload.

## What the PAYG math looks like in practice

Abstract rates are hard to feel. Here's a concrete illustration using Sharktech's published formula and current prices.

Say you take the Large plan ($249/mo, 32 cores, 64 GB RAM, 1,500 GB SSD included) and run six VMs around the clock, each sized at 8 cores, 16 GB RAM, and 150 GB SSD. Total consumption: 48 cores, 96 GB RAM, 900 GB SSD.

Storage stays within the commit, but you're over on compute and memory — 16 cores and 32 GB. At the published overage rates over a 720-hour month:

$$16 \times \$0.0025 \times 720 = \$28.80 \quad \text{(CPU)}$$

$$32 \times \$0.0035 \times 720 = \$80.64 \quad \text{(RAM)}$$

Total: $249.00 + $28.80 + $80.64 = **$358.44/mo** — with the ceiling known in advance, because the plan caps how far you can burst. If your usage is steadier than this, Dedicated Cloud's fixed pricing becomes the better deal; if it's spikier, the PAYG structure saves you from paying for peak capacity all month. Sharktech's order flow includes a calculator that quotes this per-configuration before you commit, which is the right way to compare against your current bill.

## Independent reviews and honest caveats

No provider should be evaluated on its own marketing alone. Here's what third parties say about Sharktech's cloud, from sources retrieved for this article:

- **HostAdvice's expert review** scored Sharktech Public Cloud 9.4/10 overall, with its hands-on testing reporting roughly 13,000 CPU events/sec in sysbench, memory throughput around 45.5 GB/sec, NVMe sequential reads around 5,020 MB/s, internal network speeds around 10 Gbps down / 22 Gbps up with 0.17 ms idle latency, and a support ticket answered in 39 minutes at 1 a.m. Its listed con: a limited number of global regions — five, versus dozens for the hyperscalers.
- **Trustpilot** shows a mixed 3.5/5 average across a small sample of 13 reviews, with complaints tending to cluster around early support friction and the no-refund policy rather than infrastructure failures.
- **A LowEndTalk user review** after a year of service reported Sharktech successfully mitigating sustained DDoS attacks and recommended the provider specifically for DDoS-exposed workloads.

Two policy caveats deserve plain language. First, there is **no general money-back guarantee** — payments are non-refundable, with the only exception being a billing dispute raised within 30 days that Sharktech agrees with, resolved as account credit rather than a refund. Second, payment options are broad (credit card, PayPal, wire transfer, Western Union, Alipay), which matters for international teams. The hourly billing model softens the no-refund policy considerably: you can stand up a test VM for pennies before committing to anything.

## Matching plans to real workloads

Based on the published specs, the tier-to-workload mapping is fairly clean:

- **Small ($39/mo):** staging environments, internal tools, a single production app with modest traffic. The 4-core/8 GB commit with burst to 16 cores/32 GB covers most "one important server" scenarios.
- **Medium ($79/mo):** growing SaaS backends, small Kubernetes clusters, mid-size databases. 8 cores/16 GB committed, 32 cores/64 GB on tap.
- **Large ($249/mo):** production multi-VM environments — the six-VM example above lives here. Also the natural landing spot for consolidating several scattered VPSes into one managed pool.
- **Enterprise ($499/mo):** business-critical platforms that need uncapped bursting, discounted overage rates, and serious storage headroom from day one.
- **Dedicated Cloud (from $86.23/mo):** finance-predictable environments where the monthly invoice must be identical every month, or regulated workloads that need a defined, fixed allocation.
- **Custom:** anything the standard tiers don't fit — higher compute, unusual storage ratios, or specific network needs; quoted by sales.

The genuinely useful decision rule: if your utilization curve is flat, buy fixed. If it has peaks and valleys, PAYG with a commit — which is what Sharktech's public tiers are — usually wins, and the plan caps keep the downside bounded.

## Getting started without a big commitment

Because billing is hourly on the public tiers, a realistic evaluation path costs very little: deploy a Small instance, run your workload against it for a week, and watch the actual invoice in the billing panel. The platform's weekly-updated official Linux images and cloud-init support make spin-up fast, and you can bring your own ISO if your stack is unusual.

For larger moves, Sharktech runs a **Cloud Accelerator Program** aimed at MSPs and SMEs, which includes a free assessment, a migration blueprint, and cloud credits — 👉 you can apply for it here. There's also a free consultation with their cloud team for anyone unsure which tier fits, which is the honest move when you're comparing against an incumbent hyperscaler contract: 👉 book the free cloud consultation and make them do the sizing work.

## Quick answers to common questions

**Does it support Windows?** Yes — both Linux and Windows VMs are supported, with official cloud images updated weekly for the Linux side.

**Can you scale after deployment?** Yes. CPU, RAM, and storage scale live from the management panel without rebuilding the environment, and any subscription can move up a tier without redeploying.

**Is there a minimum contract?** No. Public cloud bills hourly/monthly with no lock-in term; Dedicated Cloud offers monthly terms alongside discounted longer cycles.

**Is DDoS protection extra?** No — mitigation is built into the network on all plans, which tracks with the company's origins in DDoS-protected hosting.

**Which locations are available?** Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam, selectable at deploy time.

## The verdict

"Cloud for enterprises" resolves into a short list of questions once you strip the jargon away: which deployment model fits your compliance and performance needs, what the bill will actually look like at your usage pattern, and how expensive it is to leave if things go wrong. Hyperscalers answer those questions with scale and breadth, paid for in billing complexity and egress fees. Providers like Sharktech answer them with flat published rates, an OpenStack stack that keeps migration realistic, and a support line that a human answers — with the trade-offs being five regions instead of thirty, and a strict no-refund policy softened by hourly billing.

For mid-market enterprises, MSPs, and anyone running DDoS-exposed or cost-sensitive workloads, that trade is worth running the numbers on. The Small tier at $39/mo is a cheap experiment, and the calculator will tell you in five minutes whether the 40%-plus savings claim holds for *your* workload — which is the only version of that claim that matters.
