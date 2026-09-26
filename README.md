# ReLoop Dispute Resolution

A Python-based, rule-driven tool that reviews marketplace dispute
evidence and assigns a verdict, confidence level, and short explanation
to each case.

## Project Overview

ReLoop combines order information, carrier tracking records, and support
conversations to help triage disputes. It applies written dispute
guidelines to classify each case as:

-   **Refund** --- evidence supports refunding the buyer.
-   **Deny** --- evidence supports rejecting the claim.
-   **Escalate** --- evidence is conflicting or insufficient and needs
    human review.

The tool also flags repeat buyers and sellers for additional review.
These history flags provide context; they do not replace evidence from
the current dispute.

## Input Files

Place these files in the project folder:

-   `orders.csv` --- order details and dispute reasons.
-   `carrier_tracking.csv` --- carrier status, signature, delivery
    dates, and tracking notes.
-   `support_chat.txt` --- buyer/seller conversation evidence.
-   `Dispute_Guidelines.md` --- rules used to make decisions.
-   `Use_Case_Brief.md` --- project context and requirements.

## Requirements

-   Python 3
-   pandas
-   Jupyter Notebook (for the notebook version)

Install pandas:

``` bash
pip install pandas
```

## How to Run

1.  Keep the input files and your notebook or script in the same project
    directory.
2.  Open the notebook in Jupyter Notebook or VS Code.
3.  Run the cells from top to bottom.
4.  Review the generated decisions and validation checks.
5.  The program writes `reloop_decisions.csv` to the working directory.

For a Python script, run:

``` bash
python your_script_name.py
```

Replace `your_script_name.py` with the actual script filename.

## Output

The generated `reloop_decisions.csv` contains one row per dispute,
including:

  -----------------------------------------------------------------------
  Column                              Description
  ----------------------------------- -----------------------------------
  `order_id`                          Unique dispute/order identifier

  `buyer_handle`                      Buyer account

  `seller_handle`                     Seller account

  `dispute_reason`                    Reported dispute reason

  `verdict`                           `refund`, `deny`, or `escalate`

  `confidence`                        `high`, `medium`, or `low`

  `reason`                            Short explanation for the decision

  `evidence`                          Evidence summary used by the
                                      decision logic

  `rule_applied`                      Rule or condition that produced the
                                      verdict

  `repeat_buyer_flag`                 Whether the buyer appears in
                                      multiple records

  `repeat_seller_flag`                Whether the seller appears in
                                      multiple records

  `history_review`                    Whether either account is flagged
                                      for additional review
  -----------------------------------------------------------------------

## Decision Approach

The decision function uses ordered rules and evidence checks:

1.  **Non-delivery:** tracking that indicates the item was not delivered
    can support a refund.
2.  **Seller-acknowledged error:** an admission of a listing or
    fulfillment error can support a refund.
3.  **Confirmed receipt:** credible evidence that the buyer received the
    item can conflict with a non-receipt claim.
4.  **Conflicting or insufficient evidence:** cases that cannot be
    decided confidently are escalated.
5.  **Previously resolved issue:** a resolution accepted by both parties
    may not need to be reopened.
6.  **Seller-confirmed fault or covered damage:** explicit seller
    acknowledgment and a refund commitment can support a refund for the
    reported issue.

The implementation uses keyword and phrase matching against tracking
fields and chat text. Rules are applied in sequence, so the order of
checks matters.

## Results on the Sample Dataset

The latest run processed **20 disputes**:

  Verdict       Number of cases
  ----------- -----------------
  Refund                      8
  Deny                        1
  Escalate                   11
  **Total**              **20**

Confidence levels in that run:

  Confidence     Number of cases
  ------------ -----------------
  High                         8
  Medium                       2
  Low                         10
  **Total**               **20**

These counts describe the current sample run. They are not a measure of
model accuracy or a guarantee of performance on new disputes.

## Difficult Cases

-   **Disputed signature:** tracking records a signature, but the buyer
    says someone else signed. The case is escalated because the evidence
    conflicts.
-   **Damage during delivery:** the seller acknowledges inadequate
    packaging and promises a refund. The case is classified as a refund.
-   **Faulty item:** the seller confirms the item has a real fault and
    promises a refund. The case is classified as a refund.
-   **Delivered but not received:** a delivery scan alone may not
    establish that the buyer personally received the item, so some cases
    are escalated.

## Limitations

-   The decision logic relies on keyword and phrase matching rather than
    full understanding of conversation context.
-   Phrases can be ambiguous, negated, or used in a different context,
    which can lead to incorrect classifications.
-   The tool cannot independently verify signatures, inspect attached
    photographs, authenticate products, or establish who physically
    received a parcel.
-   The current data fields may not allow a reliable comparison between
    the address recorded at shipment and the actual delivery address.
-   Confidence labels are rule-based indicators, not statistically
    calibrated probabilities.
-   The sample contains only 20 disputes. Results should be reviewed
    before using the tool on new or real-world cases.

## Human Review

Escalated cases and low-confidence or disputed outcomes should be
reviewed by a person. The tool is intended to support consistent triage,
not to replace human judgment in ambiguous cases.

## Files to Submit

Follow the assignment's submission instructions. A typical submission
may include:

-   The completed Jupyter Notebook (`.ipynb`) or Python script (`.py`)
-   `reloop_decisions.csv`
-   This `README.md`

Include the original input files only if the assignment instructions
require them.
