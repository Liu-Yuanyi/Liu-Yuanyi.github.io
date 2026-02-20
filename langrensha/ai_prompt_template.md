# 狼人杀角色 AI 绘画提示词生成指南

这份指南旨在帮助你使用 AI 绘画工具（如 Midjourney, Stable Diffusion, DALL-E 3）生成风格统一、适配你现有网站深色 UI 的角色立绘。

## 核心设计思路

*   **风格定位**：为了配合你的网页配色（深蓝/紫背景 `#1a1a2e`），推荐使用 **"暗黑扁平插画风格" (Dark Flat Illustration)** 或 **"塔罗牌/游戏卡牌风格" (Tarot/Game Card Art)**。
*   **背景处理**：直接生成透明背景通常效果不好。建议生成 **纯色背景**（推荐使用与网页背景接近的深色或易于抠图的纯色），后期通过工具一键去底，或者直接使用深色背景融合。
*   **统一性**：保留核心关键词（风格、构图、光影），只更改角色描述。

---

## 方案 A：极简暗黑扁平风 (Flat Vector / Icon Style)
**适用场景**：替换原有的 Emoji 图标，保持网页简洁，加载快，无需抠图（直接用深色背景）。

### 提示词模板 (Prompt Template)
```text
[角色特征描述], game icon, flat vector art, minimalist style, dark fantasy theme, limited color palette (deep purple, gold, teal, crimson), clean lines, stylized, centered composition, solid dark blue background code #1a1a2e --no realistic, photo, shading, 3d
```

### 示例
*   **预言家**：`mysterious fortune teller holding a glowing crystal ball, wearing a hooded cloak, looking at viewer, game icon...`
*   **狼人**：`fearsome werewolf silhouette howling at a moon, sharp claws, glowing red eyes, game icon...`
*   **女巫**：`witch holding two potions (one purple, one green), mysterious smoke, game icon...`

---

## 方案 B：精美卡牌插画风 (Game Card / Tarot Style)
**适用场景**：想要真正的“立绘”效果，视觉冲击力强，适合放在模态框 (Modal) 或卡片封面。建议后期移除背景或使用 CSS 混合模式。

### 提示词模板 (Prompt Template)
```text
[角色特征描述], character design for werewolf card game, tarot card style, dark fantasy art, cel shaded, arcane magic atmosphere, mysterious lighting, deep colors, purple and gold color scheme, isolated on plain black background --ar 2:3 --nijiji 6 (如果用MJ)
```

*(注意：`--ar 2:3` 是纵横比，适合立绘；`--nijiji 6` 是 c 的二次元/插画模型)*

### 示例
*   **预言家**：`A mysterious hooded prophet holding a glowing magical crystal ball, distinct facial features, purple robes, mystical aura, character design for werewolf card game...`
*   **猎人**：`A rugged hunter carrying a vintage musket rifle, determined expression, leather gear, character design for werewolf card game...`
*   **丘比特**：`A mischievous winged cupid aiming a love arrow, ethereal glow, holding a bow, character design for werewolf card game...`

---

## 角色特征关键词参考表 (填入 [角色特征描述])

| 角色 | 英文关键词参考 (Character Keywords) |
| :--- | :--- |
| **预言家** | Oracle, Prophet, holding crystal ball, mystical hood, third eye, divine light |
| **女巫** | Witch, Sorceress, holding two potions (red and green), alchemy, magic smoke |
| **猎人** | Hunter, Marksman, holding a vintage rifle/gun, fedora hat, leather coat |
| **守卫** | Guardian, Knight, holding a large shield, armor, defensive stance, protecting |
| **白痴** | Fool, Jester, confused expression, colorful clothes, messy hair |
| **狼人** | Werewolf, Wolfman, sharp claws, glowing red eyes, furry, aggressive, full moon |
| **狼王** | Alpha Wolf, Wolf King, wearing a crown, majestic, fierce, fur cape |
| **丘比特** | Cupid, Angel, wings, bow and arrow, hearts, divine |

---

## 网页集成建议

为了让生成的图片完美融入你的网页：

1.  **图片处理**：
    *   使用在线工具（如 remove.bg 或 Photoshop）移除背景，保存为 `.png` 格式。
    *   或者，如果生成的背景是纯黑/深蓝，可以在 CSS 中使用 `mix-blend-mode: screen;` (滤色) 或 `lighten` 让黑色背景变透明。

2.  **CSS 更新**：
    将原来的 `.role-icon` (文字/Emoji) 改为 `<img>` 标签。

    ```css
    /* 新的图片样式建议 */
    .role-icon-img {
        width: 80px;  /* 根据需要调整 */
        height: 80px;
        object-fit: contain;
        filter: drop-shadow(0 0 5px rgba(233, 69, 96, 0.5)); /* 添加一点发光效果适配你的霓虹风 */
        transition: transform 0.3s;
    }
    
    .role-card:hover .role-icon-img {
        transform: scale(1.1);
    }
    ```
