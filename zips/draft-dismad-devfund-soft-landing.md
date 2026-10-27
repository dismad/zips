```
ZIP: Unassigned
Title: Dev Fund Soft Landing
Owners: dismad <dismad@zechub.social>
Status: Draft
Category: Consensus / Process
Created: 2026-10-26
License: MIT
Discussions-To: <https://forum.zcashcommunity.com/t/draft-zip-dev-fund-soft-landing/58519>
Pull-Request: <https://github.com/zcash/zips/pull/XXXX>
```

# Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [1] when, and only when, they appear in all capitals.

The terms "Mainnet" and "Testnet" are to be interpreted as described in § 3.12 ‘Mainnet and Testnet’ of the Zcash Protocol Specification [2].

The term "halving height" refers to the block height at which the block subsidy halves, as defined by the Zcash protocol (including the adjustment specified by ZIP 218 [3] if NU7 activates before the third halving).

# Abstract

This ZIP defines a successor schedule to the funding streams established by ZIP 1016 [4]. It leaves the governance, voting, multisig, veto, and disbursement rules of ZIP 1016 and ZIP 271 [5] unchanged, and only reduces the percentages of the Zcash Community Grants (ZCG) and Coinholder-Controlled Fund streams at successive halving heights.

The schedule is:

| Period | ZCG | Coinholder Fund | Total | Miner |
| --- | --- | --- | --- | --- |
| Until 3rd halving | 8% | 12% | 20% | 80% |
| 3rd → 4th halving | 4% | 6% | 10% | 90% |
| 4th → 5th halving | 2% | 3% | 5% | 95% |
| After 5th halving | 0% | 0% | 0% | 100% |

# Motivation

ZIP 1016 established an 8% ZCG stream and a 12% Coinholder-Controlled Fund stream that run until the third half. Without a successor, those streams end and 100% of the block subsidy returns to miners.

This ZIP provides a minimal, deterministic taper that:

- Continues the existing mechanisms at reduced intake levels.
- Gives the ecosystem a multi-year wind-down period.
- Removes the open-ended 20% commitment after a defined number of halves.
- Requires no new governance rules, voting processes, or Key-Holder obligations.

# Requirements

- The ZCG and Coinholder-Controlled Fund mechanisms defined by ZIP 1016 and ZIP 271 MUST continue to operate unchanged except for the reduced funding-stream percentages specified in this ZIP.
- The 2:3 ratio between the ZCG stream and the Coinholder-Controlled Fund stream MUST be preserved in every period.
- All height boundaries MUST be expressed relative to the actual half heights (including any NU7 spacing adjustment from ZIP 218).
- No new consensus rules beyond the funding-stream percentages are required.

# Non-requirements

- This ZIP does not alter the voting threshold, quorum, review period, veto rules, or Key-Holder obligations of ZIP 1016.
- This ZIP does not introduce a permanent floor, a review gate, or any other discretionary mechanism.
- This ZIP does not change the rules governing the Deferred Dev Fund Lockbox or the one-time disbursement specified by ZIP 271.

# Specification

The funding streams defined by ZIP 214 Revision 3 [6] and extended by ZIP 1016 are modified as follows.

Let \( H_3 \) be the third-half height, \( H_4 \) the fourth-half height, and \( H_5 \) the fifth-half height, each computed according to the protocol (including ZIP 218 if applicable).

| Stream | Numerator | Denominator | Start height | End height |
| --- | --- | --- | --- | --- |
| FS_FPF_ZCG_H3 | 8 | 100 | (existing) | \( H_3 \) |
| FS_CCF_H3 | 12 | 100 | (existing) | \( H_3 \) |
| FS_FPF_ZCG_H4 | 4 | 100 | \( H_3 \) | \( H_4 \) |
| FS_CCF_H4 | 6 | 100 | \( H_3 \) | \( H_4 \) |
| FS_FPF_ZCG_H5 | 2 | 100 | \( H_4 \) | \( H_5 \) |
| FS_CCF_H5 | 3 | 100 | \( H_4 \) | \( H_5 \) |

After height \( H_5 \), no further funding streams for ZCG or the Coinholder-Controlled Fund are defined by this ZIP. The remainder of the block subsidy is allocated to miners.

All other rules of ZIP 1016 (voting, review period, 420 000 ZEC threshold, simple majority, Key-Holder obligations, veto process) and ZIP 271 (multisig, disbursement, ability to leave funds at rest) continue to apply to any funds that have already been received or that continue to be received under the streams above.

# Rationale

Stepping the percentages down at the known half heights is the smallest consensus change that produces a predictable reduction. It reuses the existing ZIP 214 funding-stream table format and requires no new opcodes, voting mechanisms, or governance processes.

Preserving the 2:3 ratio ensures that both the community-grant and coinholder-grant pathways scale down together.

Expressing boundaries as relative heights avoids hard-coding constants that would become incorrect if the NU7 spacing adjustment changes the exact third-half height.

# Deployment

This ZIP is intended to be deployed so that the first step-down (from 8%/12% to 4%/6%) takes effect at the third-half height. Exact activation height and network-upgrade coordination are left to the ZIP that defines the corresponding Network Upgrade.

# Open issues

- Should a permanent floor (for example 1% + 1.5%) be added after the fifth half instead of a hard zero?
- Should the schedule extend one more period (5th → 6th half) before reaching zero?
- Are the chosen step sizes (20% → 10% → 5% → 0%) the preferred reduction rates?
- Should any review or replacement mechanism be added, or is the “future ZIP can still replace this schedule” stance sufficient?

# References

1. [BCP 14](https://www.rfc-editor.org/info/bcp14)
2. [Zcash Protocol Specification](https://zips.z.cash/protocol/protocol.pdf)
3. [ZIP 218: 25-second Block Target Spacing](https://zips.z.cash/zip-0218)
4. [ZIP 1016: Community and Coinholder Funding Model](https://zips.z.cash/zip-1016)
5. [ZIP 271: Dev Fund Extension and One-Time Disbursement](https://zips.z.cash/zip-0271)
6. [ZIP 214: Consensus rules for a Zcash Development Fund](https://zips.z.cash/zip-0214)
