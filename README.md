Example base file: v50.03 `entity_default.txt`  
Assumed header for examples: `[OBJECT:ENTITY] [SELECT_ENTITY:MOUNTAIN]`  
The following tokens are proposed to allow additional freedom to mods. This proposal adds tokens that modify existing tokens.

1. A token `[SELECT_TOKEN:name:...args]` that... selects tokens. The token selected must be named `name`, and will have the arguments `args`. The special arguments `*` and `...` are treated specially in `args`: `*` matches any argument, and `...` matches multiple arguments of any value. `args` defaults to `...`. In case of multiple matches, the first one will be used and a warning will be printed. Example: `[SELECT_TOKEN:WEAPON]` would match `[WEAPON:ITEM_WEAPON_AXE_BATTLE]` on line 11 and print a warning, `[SELECT_TOKEN:GLOVES:*:UNCOMMON]` would match `[PANTS:ITEM_PANTS_BRAIES:UNCOMMON]` on line 46.

2. A token `[SPLICE_TOKEN:position:count:...args]`: Starting at the argument `position` (where the first argument is 1), remove `count` arguments, then insert `args` in place of the removed arguments. Example: If `[PANTS:ITEM_PANTS_BRAIES:UNCOMMON]` is selected and `[SPLICE_TOKEN:2:1:COMMON]` is used, the resulting token would be `[PANTS:ITEM_PANTS_BRAIES:COMMON]`. Multiple `[SPLICE_TOKEN]`s to the same argument would fail.

3. A token `[REMOVE_TOKEN]`: Removes the current token. The token selection is *cleared*.
