---
# prettier-ignore
date: 2025-11-21
title: Fix Neo Tree Jumping Cursor Completely
description: A complete way to fix the jumping cursor problem in Neo-tree.
tags:
  - Neovim
  - nixvim
---

## Background

In my [previous post](../fix-neo-tree-jumping-cursor), I shared the method of fixing jumping cursor in Neo-tree by focusing node after the `open` command.

However, after a period of time, I found that the issue occurred again when I used `yank / copy` operation. So I had to debug it again.

## Reason

Since I had changed the `open` command and the issue was still remaining there, so the problem is not on `open` command, but on `close_node` command.

I bind `h` to `close_node` action, and it seems that Neo-tree won't refresh its state after calling `close_node`, which produced this issue.

## Solution

After knowing the reason, the solution is simple, where Neo-tree should refresh its state after calling `close_node` operation.

My approach is to define a custom commands called `close_node_with_refresh` and bind it to `h`.

The command looks like:

```lua
function(state)
  local tree = state.tree
  local node = assert(tree:get_node())
  require("neo-tree.sources.common.commands").close_node(state)
  require("neo-tree.sources.manager").refresh(state.name)
end
```

And in `nixvim`, we can easily define and bind this command to `h`.

```nix
{...}: {
  plugins.neo-tree = {
    enable = true;

    settings = {
      commands = {
        close_node_with_refresh.__raw = ''
          function(state)
            local tree = state.tree
            local node = assert(tree:get_node())
            require("neo-tree.sources.common.commands").close_node(state)
            require("neo-tree.sources.manager").refresh(state.name)
          end,
        '';
      };
      window.mappings = {
        "h" = "close_node_with_refresh";
      };
    };
  };
}
```

After this, Neo-tree will work as expected.
