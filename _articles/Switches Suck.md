---
title: Switches Suck
date: 2019-02-15 00:53:00 -0800
modified: 
permalink: /switches-suck/
category: Programming
blags: [Lua, programming style, programming tips, tips]
tags: writing/blog/published
---

I don't like switch statements, in any language. They seem unnecessarily verbose and error-prone, in fact I forgot the break statements in my example below on the first draft. Most of the time, you _don't_ want the fall-through feature, but you have to remember that extra word for each case to prevent that.

```
switch (n)
{
    case 1:
    // something useful
    break;
    case 2:
    // another useful option
    break;
    default:
    // nothing matched
}
```

I also really hate the indenting used in most examples (including my own), as it makes it more difficult to visually parse. I prefer to just create an object with keys based on the possible values, and access what you need directly.

```
-- we're gonna pretend these are useful functions dependent on a star's type..something to do with heat?
local default = {}           -- used for a unique key
local heat = {
  A = function() end,        -- pretend these are full of useful code
  B = function() end,
  G = function() end,        -- and so on
  [default] = function() end -- default which can't be accidentally chosen
}

-- make sure we don't error, and call default if needed
if heat[star.type] then
  heat[star.type]()
else
  heat[default]()
end
```
