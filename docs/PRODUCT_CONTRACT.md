# Meal Planner MVP Product Contract

## Goal

Build a Factor-style weekly recipe selector that turns a small curated menu into a realistic low-prep meal plan backed by real recipe sources, transparent nutrition evidence, and timestamped grocery estimates.

The first release is a public demo and recipe catalog with a private personal planning surface.

## Locked decisions

- The repository and reviewed recipe catalog are public.
- Personal selections, inventory, receipts, store details, adherence notes, and meal history are private.
- A week contains two selected lunch recipes and two selected dinner recipes.
- Lunch and dinner each use a 4 + 3 rotation, producing fourteen weekly meal allocations from four recipes.
- Eligible meals favor slow cookers, one-pot methods, sheet pans, dump-and-cook methods, and minimal assembly.
- Inherently very spicy recipes and mac-and-cheese-based meals are excluded.
- Core recipes must come from real, directly linked sources.

## Weekly user flow

1. A scheduled Discord prompt tells the user that the next menu is ready and links to the selector.
2. The selector displays a curated pool of approximately eight to twelve eligible meal cards, separated into lunch and dinner candidates.
3. The user selects two lunch recipes and two dinner recipes.
4. The planner maps the first selection in each lane to four days and the second to three days.
5. The planner recalculates required recipe scale and plan servings instead of assuming the source serving matches the user's allocation.
6. The planner merges ingredients across all four recipes.
7. Confirmed private inventory may reduce the purchase list. Projected leftovers may not.
8. A store-scoped RCSS estimate is refreshed for the locked shortlist.
9. The app presents checkout cost, consumed-food cost, paid carryover, substitutions, and evidence timestamps separately.
10. The user explicitly approves or rejects the proposed week. Nothing is treated as active before approval.

## Meal-card contract

Every public recipe card must include:

- stable recipe identifier
- visible meal name
- canonical source URL
- creator or publisher
- source verification date
- thumbnail provenance and fallback status
- source yield
- source serving basis
- source-listed calories when available
- planner-calculated calories and confidence when available
- active prep time and total time
- equipment
- main ingredient count
- dietary and preparation tags
- spice classification
- source confidence state
- nutrition confidence state

Useful optional fields include protein, fibre, sodium, freezer suitability, reheating notes, package-use notes, rating evidence, and first-hand preparation review.

## Eligibility policy

Default targets:

- eight or fewer main ingredients
- soft ceiling of ten main ingredients
- fifteen minutes or less active prep
- no mandatory advanced technique
- no repeated pan transfers unless the meal remains meaningfully low effort
- one primary cooking vessel when practical

Salt, pepper, water, and ordinary cooking oil do not count toward the headline ingredient count, but they must still appear in cooking and nutrition calculations when relevant.

A meal is excluded when it is fundamentally very spicy, fundamentally mac-and-cheese based, missing a direct original source, unsafe for the intended storage cadence, or too incomplete to reproduce reliably.

## Source states

Recipes move through explicit states:

- `discovered`: potentially relevant source found
- `screened`: source identity, yield, ingredients, and method checked
- `provisional`: suitable for a proposed menu but awaiting exact product or real-preparation evidence
- `validated`: source, adaptation, nutrition basis, storage, and at least one real preparation review are reconciled
- `rejected`: provenance, preference, safety, or reproducibility failure

A TikTok recipe may be a valid direct source when the original creator, canonical post, quantities, yield, and method are recoverable. A visually appealing concept without reproducible quantities remains `discovered` and cannot enter an active week.

## Attribution and image policy

- Link directly to the original source.
- Preserve creator or publisher attribution.
- Do not copy expressive source instructions verbatim when a concise attributed adaptation is sufficient.
- Do not copy or redistribute source photography unless the license or permission allows it.
- Remote source thumbnails may be used only when technically and contractually appropriate.
- Otherwise use original, generated, or neutral fallback artwork with clear provenance.

## Nutrition policy

- Display source-listed calories as source data, not as verified fact.
- Display planner-calculated nutrition separately and include the serving basis.
- Recalculate adaptations, sides, oils, sauces, and changed package quantities.
- Do not use health claims or personalized targets in the public demo.
- Keep personal calorie targets and health constraints in private configuration.
- Treat nutrition as an estimate until tied to exact products and actual yield.

## Grocery estimate policy

The private planner may target a configured RCSS store. Evidence must distinguish:

- exact product identity
- retailer-level listing
- store-scoped price
- store-scoped availability
- exact nutrition label or fallback nutrition source
- verification timestamp

The UI must show whole-package checkout separately from estimated consumed-food cost and paid carryover. Variable-weight items must be modeled transparently and reconciled from the receipt. Generic `InStock` metadata cannot be presented as proof of availability at the configured store.

## Privacy boundary

Never publish or commit:

- personal weekly selections
- inventory and package remainders
- receipts
- postal code or private store configuration
- adherence, health, or weight notes
- personal calorie targets
- private retailer evidence caches
- credentials, cookies, tokens, or authenticated browser state

The public demo must use fixtures. Automated tests must verify that private paths and representative sensitive fields cannot enter public build artifacts.

## Suggested product improvements

### Explain why each meal was selected

Show concise reason chips such as `9 min prep`, `slow cooker`, `high protein`, `uses pantry rice`, or `freezer friendly`. Curation should feel intentional rather than random.

### Separate source serving from plan serving

A source recipe's 420-calorie serving may not satisfy a two-meal-day allocation. The UI should show both values and explain scaling.

### Optimize across the full four-recipe basket

Rank menus partly by shared ingredients and complete-package use. Four individually cheap meals can create an expensive cart when they require unrelated sauces and perishables.

### Preserve approval gates

The weekly prompt opens selection. Selection creates a proposal. A fresh price check and explicit approval activate the plan. No purchase, substitution, or plan activation is implied automatically.

### Learn from real outcomes

After preparation, record private ratings for taste, effort, portion size, reheating quality, waste, and whether the recipe should repeat. These observations should influence future curation without being published.

## MVP acceptance criteria

The MVP is accepted only when it demonstrates all of the following with automated tests and a real bounded pilot:

1. Load a public catalog containing at least twelve source-backed recipe records.
2. Reject records missing required provenance or violating hard preference exclusions.
3. Render Factor-style responsive cards with safe image fallbacks.
4. Filter and select exactly two lunch recipes and two dinner recipes.
5. Generate a deterministic 4 + 3 weekly allocation for both meal lanes.
6. Scale recipe quantities from source yield to required allocations.
7. Merge duplicate shopping ingredients with normalized units where safe.
8. Display source calories separately from calculated plan calories.
9. Display timestamped sample grocery evidence without implying live stock.
10. Keep all real personal state outside the public demo and repository.
11. Export a complete proposed-week artifact containing selections, schedule, shopping list, cooking summaries, and original links.
12. Require explicit approval before marking a private week active.
13. Pass independent specification, quality, security, privacy, accessibility, and integration reviews.
14. Complete one real weekly pilot using four selected recipes and capture discrepancies for the next iteration.

## Non-goals for the first release

- automatic grocery purchasing
- medical nutrition advice
- calorie tracking as a replacement for professional guidance
- social accounts or multi-user collaboration
- copying full copyrighted recipe articles or unlicensed photography
- claiming exact live inventory without store-scoped evidence
- native mobile apps before the web workflow proves useful
- autonomous activation of a weekly plan

## Open operational setting

The weekly Discord prompt time remains configurable. It should occur early enough to choose recipes, refresh prices, and approve the packet before the normal shopping and preparation window.
