# Meal Planner

A source-verified, health-centric weekly meal selector for people who want Factor-style choice without subscription pricing.

Meal Planner curates easy, low-prep recipes from real sources, presents them as visual meal cards, and turns four weekly selections into a practical 4 + 3 lunch and dinner rotation.

## Product direction

Each weekly menu offers a small, reviewed collection of lunch and dinner cards. A card includes:

- meal name and an attributable thumbnail or safe fallback artwork
- original creator or publisher and a direct source link
- calories per source serving and, when available, a separately calculated plan serving
- active prep time, total time, equipment, yield, and ingredient count
- tags such as slow cooker, one pot, sheet pan, freezer friendly, and minimal prep
- source confidence and nutrition confidence

The weekly flow asks the user to choose:

- two lunch recipes
- two dinner recipes
- a 4 + 3 allocation for each meal lane

After selection, Meal Planner produces a merged shopping list, a timestamped grocery estimate, cooking instructions with source links, and a private weekly plan.

## Recipe principles

Eligible recipes should normally have eight or fewer main ingredients, require no more than fifteen minutes of active preparation, and favor slow cookers, one-pot meals, sheet-pan meals, or simple assembly.

The initial preference policy excludes:

- recipes that are inherently very spicy
- mac-and-cheese-based meals
- unsourced or invented core recipes
- social-media concepts without enough information to verify quantities, yield, and method

## Public and private boundary

This repository and its reviewed recipe catalog are public. The public demo uses fixtures or sample data.

Personal selections, inventory, receipts, store configuration, price history, adherence notes, and meal history remain private. They must not be committed to the public repository.

## Evidence policy

Meal Planner distinguishes:

- original recipe provenance
- source-listed nutrition
- planner-calculated nutrition
- retailer listing evidence
- store-scoped price and availability evidence
- modeled checkout cost versus consumed-food cost

Prices and inventory are estimates tied to a store and verification time. A proposed week does not become active until the user approves it.

## Status

Product contract established. Implementation will be used as the bounded end-to-end pilot for Revision Yard after Revision Yard passes its own acceptance gate.

See [`docs/PRODUCT_CONTRACT.md`](docs/PRODUCT_CONTRACT.md) for the MVP requirements and acceptance criteria.

## License

MIT
