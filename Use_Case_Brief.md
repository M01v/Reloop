# Pre-Interview Project: Dispute Resolution

## The situation

ReLoop is a resale marketplace. When a buyer disputes an order — never arrived, wrong item,
arrived broken — someone has to decide who's right. Right now a person reads three different
systems by hand for every case. We want to see what you'd build to make that faster, without
making it worse.

**Attached:**
- `orders.csv` — the disputed orders themselves
- `carrier_tracking.csv` — what the carrier's system says happened to each package
- `support_chat.txt` — the actual conversation for each dispute
- `Dispute_Guidelines.md` — the policy whoever resolves these is supposed to follow

20 real-shaped disputes. Some are straightforward. Some aren't — and the guidelines above say
what to do when they aren't.

## What we want back

**1. A working tool.** Something that reads the three data files and produces, per dispute: a
verdict (refund / deny / escalate), a confidence level, and a short reason. Doesn't matter what
you build it in — script, notebook, small app — but it should actually run, not just describe
what it would do.

Build it to handle **new disputes it hasn't seen**, not just these 20. We'll hand your tool a
few new cases during the call and see what it does with them.

**2. A short write-up.** A few bullet points is fine:
   - Any pattern you noticed in where a simple rule would get things wrong
   - The specific cases you were least confident about, and why
   - Anything the data genuinely doesn't let you resolve

## Ground rules

- **Budget 4–5 hours.** We mean it — this isn't scored on polish or on how much you built, and
  going well over won't score higher.
- **Use any tool you want, including AI assistants.** How you use them is more interesting to us
  than whether you did.
- **If a case is genuinely ambiguous, say so in the output.** "Escalate — insufficient evidence"
  is a legitimate verdict. A confident guess is not better than an honest one.

## What happens next

Send back whatever you built before the call. We'll run it live on a few cases you haven't seen,
and walk through some of the calls it made — including asking you to defend specific ones.
