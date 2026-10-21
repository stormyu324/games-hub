# Storm Nova Games 游戏大厅

https://games.stormnovalabs.com/ 的首页，列出所有小游戏。

只是一个静态页面（`public/index.html`），部署成 Cloudflare Worker `games-hub`，
**只接管 `games.stormnovalabs.com/` 这一个根路径**，各个游戏的路径由它们自己的 Worker 处理：

| 路径 / 域名 | Worker | 仓库 |
|---|---|---|
| `games.stormnovalabs.com/` | `games-hub` | 本仓库 |
| `games.stormnovalabs.com/cards-cursor/` | `games` | cards-cursor |
| `games.stormnovalabs.com/majiang/` | `majiang` | simple-majiang |
| `games.stormnovalabs.com/kart/` | `kart-rush` | kart-rush |
| `games.stormnovalabs.com/rts/` | `steel-front` | steel-front |

## 部署

```bash
npx wrangler login    # 第一次需要登录
npx wrangler deploy
```

## 加一个新游戏

1. 新游戏用自己的 Worker，路由设成 `games.stormnovalabs.com/<名字>` 和 `games.stormnovalabs.com/<名字>/*`
   （更具体的路径路由会优先于 `games` 的自定义域名，不影响其他游戏）
2. 在 `public/index.html` 里加一张卡片，然后重新部署本仓库
