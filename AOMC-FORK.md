# AOMC-ChestShop adaptation

Established October 14, 2026 for Avatar Origins MC.

- Upstream: https://github.com/QuickShop-Community/QuickShop-Hikari
- Fork: https://github.com/bobcat4848/AOMC-ChestShop
- Baseline: `824348433c47e0edeba8f2f896855b59fa3d29ab` on upstream `hikari`.
- AOMC development branch: `aomc`; upstream remains available as the `upstream` remote.

## Status

This is a source fork and adaptation plan, not a functioning AOMC release. No
production configuration, binary branding, cash provider or Character ownership
patch has been enabled by this foundation commit. Preserve upstream Java/API
structure initially so focused patches remain maintainable across upstream merges.

## Confirmed storefront contract

1. A buyer must carry sufficient valid physical Yuan in ordinary inventory.
   Character/Account bank funds never substitute automatically.
2. Proceeds appear as valid physical coins in the shop's recorded owning Character
   bank, including while the owner is offline or another Character is selected.
   Bank coins are not simultaneously a second spendable balance. Full-bank payouts
   remain saved for later placement; cap pending payouts and pause further sales
   before capacity is exceeded. The owning Minecraft account
   remains an authentication identity; it is not a substitute for the Character owner.
3. Validate genuine coin/bill identities, combine supported denominations, consume
   spent notes once and issue exact valid change. A configured item template must
   never recreate note serials or stand in for currency validation.
4. Cash purchase is a transfer, not money issuance or a server sink. One durable
   purchase operation coordinates stock reservation, cash consumption, seller credit,
   change and goods recovery. A generic cash deduction followed by a separate bank
   deposit does not satisfy this contract.
5. Transfer the actual deposited item, preserving quality, wear, maker, bindings,
   upgrade state and all authoritative metadata. A display template is not stock.
6. Shop management requires the recorded owning Character and valid property
   authority. Offline sales remain available without granting another Character
   editing or stock access.
7. Purchases happen at registered physical storefronts. A free AOMC directory
   provides discovery and directions. The separate shared Exchange retains its
   confirmed seller-paid 25% fee, rounded down to whole Yuan and entirely destroyed
   as a server sink. Checkouts/fills of 1–3 Yuan have no Exchange fee. Physical
   player-shop sales have a confirmed 0% commission.
8. Teleport/browse permissions cannot provide universal free warps or bypass
   active Logistics shipments, combat checks, travel scrolls or the chosen timed
   transport rules. Review upstream teleport/tag commands and default grants.
9. Keep unrelated plugins' bank-funded payment semantics. Scope carried-cash-only
   storefront checkout to AOMC-ChestShop. The unified physical item-bank conversion
   needs its own currency-service/Vault migration; do not count stored coins and
   a legacy numerical balance as the same value twice.

## Integration boundaries

Keep AOMC-specific stock/payment/permission changes isolated where possible.
The persisted shop extra-data map is a candidate for the Character owner, subject
to migration and lifecycle tests. The trade service and economy integration are
candidate checkout boundaries; correctness takes precedence over an addon-only
implementation.

Default upstream owner transfers, split beneficiaries, taxes, remote purchase
paths and ender-chest stock integrations must be reviewed before an AOMC release.
Keep separately deposited shop and Exchange stock unless both channels share a
single proven reservation/recovery protocol. Planned stockpiles feed registered
premises or an approved local warehouse; a global bank page is not an automatic
stockpile link. Restocking moves ordinary bankable goods into shop custody once.
Registered mission cargo is excluded.

## Acceptance before release

- Carried cash is insufficient even when the buyer bank has ample funds: no sale.
- Mixed denominations, exact payment and overpayment produce conserved value.
- Offline owner, Character switch and stale interaction pay the recorded owner only.
- Copied/redeemed note identities cannot fund another sale; change remains valid.
- Concurrent checkout cannot sell the same stock twice.
- Restart/disconnect at each payment/stock boundary produces recoverable obligations.
- Full buyer inventory preserves paid goods and change for later recovery.
- A forged item with unique maker/wear/upgrade data arrives unchanged.
- Property closure or membership changes preserve unsold stock and paid entitlements.
- Default shop teleports do not bypass the travel service or shipment restriction.
- A normal cash death drop preserves the bearer identities and face value. It
  cannot create a refund or bank credit for money that remained carried.
- A 90-Yuan storefront sale credits 90 to its owner; no sale commission is taken.
- Offline proceeds land as physical coins in the recorded Character bank; a full
  bank cannot lose payout or create unlimited uncollected cash capacity.

## Attribution and source

Retain the upstream LICENSE, EULA, copyright and contributor notices. The upstream
license file states GPLv3/AGPLv3 dual licensing and AGPLv3 for additions after
June 29, 2024. Preserve those terms and identify AOMC modifications with dates.
An eventual modified running release must provide the corresponding source link
to network users as required by the applicable license. The upstream EULA is
retained; this plan does not resolve any disagreement among upstream notices.

Upstream support is not responsible for AOMC-specific patches. Build/deployment,
source availability and a complete gameplay test remain release gates.
