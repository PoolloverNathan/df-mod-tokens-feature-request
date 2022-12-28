Example base file: v50.03 [`entity_default.txt`](/entity_default.txt)  
Assumed header for examples: `[OBJECT:ENTITY] [SELECT_ENTITY:MOUNTAIN]`  
The following tokens are proposed to allow additional freedom to mods. This proposal adds tokens that modify existing tokens.

1. A token `[SELECT_TOKEN:name:...args]` that selects tokens.
   The token selected must be named `name`, and will have the arguments `args`. The special arguments `*` and `...` are treated specially in `args`: `*` matches any argument, and `...` matches multiple arguments of any value. `args` defaults to `...`. In case of multiple matches, the first one will be used, but this can be modified by `[START_TOKEN]`. If there are zero matches, a loading error will occur.
   Example:
   * `[SELECT_TOKEN:WEAPON]` would match `[WEAPON:ITEM_WEAPON_AXE_BATTLE]` on line 11 and print a warning
   * `[SELECT_TOKEN:GLOVES:*:UNCOMMON]` would match `[PANTS:ITEM_PANTS_BRAIES:UNCOMMON]` on line 46.
   * `[SELECT_TOKEN:PANTS:ITEM_PANTS_GREAVES]` would **not** match `[PANTS:ITEM_PANTS_GREAVES:COMMON]`. However, `[SELECT_TOKEN:PANTS:ITEM_PANTS_GREAVES:*]` or `[SELECT_TOKEN:PANTS:ITEM_PANTS_GREAVES:...]` would; hovever, `[SELECT_TOKEN:PANTS:...]` would match `[PANTS:ITEM_PANTS_PANTS:COMMON]`.
   
1. A token `[SPLICE_TOKEN:position:count:...args]`
   Starting at the argument `position` (where the first argument is 1), remove `count` arguments, then insert `args` in place of the removed arguments. Multiple `[SPLICE_TOKEN]`s to the same argument would fail.  
   Example:
   * If `[PANTS:ITEM_PANTS_BRAIES:UNCOMMON]` is selected and `[SPLICE_TOKEN:2:1:COMMON]` is used, the resulting token would be `[PANTS:ITEM_PANTS_BRAIES:COMMON]`.

1. A token `[CUT_TOKEN]`
   Removes the current token. The token selection is *cleared*.
   Example:
   * Using `[SELECT_TOKEN:PERMITTED_JOB:MINER]` then `[CUT_TOKEN]` would prevent mining. This is a bad idea.
