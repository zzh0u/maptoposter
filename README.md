# 城市地图海报生成器

为世界任何城市生成美观、简约的地图海报。

## 安装

### 使用 uv（推荐）

确保已安装 [uv](https://docs.astral.sh/uv/)。在脚本前加上 `uv run` 会自动创建和管理虚拟环境。

测试尺寸

```bash
uv run ./create_map_poster.py --city 'Changsha' --country China --width 12.8 --height 7.2 --distance 15000
```

生成

```bash
uv run ./create_map_poster.py --city 'Changsha' --country China --all-themes --width 12.8 --height 7.2 --distance 30000
```

### 必需选项

| 选项 | 短选项 | 描述 |
|--------|-------|-------------|
| `--city` | `-c` | 城市名称（用于地理编码） |
| `--country` | `-C` | 国家名称（用于地理编码） |

### 可选标志

| 选项 | 短选项 | 描述 | 默认值 |
|--------|-------|-------------|---------|
| **OPTIONAL:** `--latitude` | `-lat` | 覆盖纬度中心点（与 --longitude 一起使用） | |
| **OPTIONAL:** `--longitude` | `-long` | 覆盖经度中心点（与 --latitude 一起使用） | |
| **OPTIONAL:** `--country-label` | | 覆盖海报上显示的国家文本 | |
| **OPTIONAL:** `--theme` | `-t` | 主题名称 | terracotta |
| **OPTIONAL:** `--distance` | `-d` | 地图半径（米） | 18000 |
| **OPTIONAL:** `--list-themes` | | 列出所有可用主题 | |
| **OPTIONAL:** `--all-themes` | | 为所有可用主题生成海报 | |
| **OPTIONAL:** `--width` | `-W` | 图像宽度（英寸） | 12 (最大: 20) |
| **OPTIONAL:** `--height` | `-H` | 图像高度（英寸） | 16 (最大: 20) |

### 多语言支持 - i18n

使用来自 Google Fonts 的自定义字体以您的语言显示城市和国家名称：

| 选项 | 短选项 | 描述 |
|--------|-------|-------------|
| `--display-city` | `-dc` | 城市自定义显示名称（例如："東京"） |
| `--display-country` | `-dC` | 国家自定义显示名称（例如："日本"） |
| `--font-family` | | Google Fonts 字体族名称（例如："Noto Sans JP"） |

**示例：**

```bash
# 日语
python create_map_poster.py -c "Tokyo" -C "Japan" -dc "東京" -dC "日本" --font-family "Noto Sans JP"

# 韩语
python create_map_poster.py -c "Seoul" -C "South Korea" -dc "서울" -dC "대한민국" --font-family "Noto Sans KR"

# 阿拉伯语
python create_map_poster.py -c "Dubai" -C "UAE" -dc "دبي" -dC "الإمارات" --font-family "Cairo"
```

**注意**：字体会自动从 Google Fonts 下载并缓存在本地 `fonts/cache/` 目录中。

### 分辨率指南（300 DPI）

使用以下 `-W` 和 `-H` 值以定位特定分辨率：

| 目标 | 分辨率（像素） | 英寸（-W / -H） |
|--------|-----------------|------------------|
| **Instagram 帖子** | 1080 x 1080 | 3.6 x 3.6 |
| **手机壁纸** | 1080 x 1920 | 3.6 x 6.4 |
| **高清壁纸** | 1920 x 1080 | 6.4 x 3.6 |
| **4K 壁纸** | 3840 x 2160 | 12.8 x 7.2 |
| **A4 打印** | 2480 x 3508 | 8.3 x 11.7 |

### 使用示例

#### 基本示例

```bash
# 使用默认主题的简单用法
python create_map_poster.py -c "Paris" -C "France"

# 使用自定义主题和距离
python create_map_poster.py -c "New York" -C "USA" -t noir -d 12000
```

#### 多语言示例（非拉丁文字）

以原生文字显示城市名称：

```bash
# 日语
python create_map_poster.py -c "Tokyo" -C "Japan" -dc "東京" -dC "日本" --font-family "Noto Sans JP" -t japanese_ink

# 韩语
python create_map_poster.py -c "Seoul" -C "South Korea" -dc "서울" -dC "대한민국" --font-family "Noto Sans KR" -t midnight_blue

# Thai
python create_map_poster.py -c "Bangkok" -C "Thailand" -dc "กรุงเทพมหานคร" -dC "ประเทศไทย" --font-family "Noto Sans Thai" -t sunset

# 阿拉伯语
python create_map_poster.py -c "Dubai" -C "UAE" -dc "دبي" -dC "الإمارات" --font-family "Cairo" -t terracotta

# Chinese (Simplified)
python create_map_poster.py -c "Beijing" -C "China" -dc "北京" -dC "中国" --font-family "Noto Sans SC"

# Khmer
python create_map_poster.py -c "Phnom Penh" -C "Cambodia" -dc "ភ្នំពេញ" -dC "កម្ពុជា" --font-family "Noto Sans Khmer"
```

#### 高级示例

```bash
# Iconic grid patterns
python create_map_poster.py -c "New York" -C "USA" -t noir -d 12000           # Manhattan grid
python create_map_poster.py -c "Barcelona" -C "Spain" -t warm_beige -d 8000   # Eixample district

# Waterfront & canals
python create_map_poster.py -c "Venice" -C "Italy" -t blueprint -d 4000       # Canal network
python create_map_poster.py -c "Amsterdam" -C "Netherlands" -t ocean -d 6000  # Concentric canals
python create_map_poster.py -c "Dubai" -C "UAE" -t midnight_blue -d 15000     # Palm & coastline

# Radial patterns
python create_map_poster.py -c "Paris" -C "France" -t pastel_dream -d 10000   # Haussmann boulevards
python create_map_poster.py -c "Moscow" -C "Russia" -t noir -d 12000          # Ring roads

# Organic old cities
python create_map_poster.py -c "Tokyo" -C "Japan" -t japanese_ink -d 15000    # Dense organic streets
python create_map_poster.py -c "Marrakech" -C "Morocco" -t terracotta -d 5000 # Medina maze
python create_map_poster.py -c "Rome" -C "Italy" -t warm_beige -d 8000        # Ancient layout

# Coastal cities
python create_map_poster.py -c "San Francisco" -C "USA" -t sunset -d 10000    # Peninsula grid
python create_map_poster.py -c "Sydney" -C "Australia" -t ocean -d 12000      # Harbor city

# River cities
python create_map_poster.py -c "London" -C "UK" -t noir -d 15000              # Thames curves
python create_map_poster.py -c "Budapest" -C "Hungary" -t copper_patina -d 8000  # Danube split

# Override center coordinates
python create_map_poster.py --city "New York" --country "USA" -lat 40.776676 -long -73.971321 -t noir

# List available themes
python create_map_poster.py --list-themes

# Generate posters for every theme
python create_map_poster.py -c "Tokyo" -C "Japan" --all-themes
```

### 距离指南

| 距离 | 最适合 |
|----------|----------|
| 4000-6000m | Small/dense cities (Venice, Amsterdam center) |
| 8000-12000m | Medium cities, focused downtown (Paris, Barcelona) |
| 15000-20000m | Large metros, full city view (Tokyo, Mumbai) |

## 主题

14 themes available in `themes/` directory:

| 主题 | 风格 |
|-------|-------|
| `noir` | Pure black background, white roads |
| `midnight_blue` | Navy background with gold roads |
| `blueprint` | Architectural blueprint aesthetic |
| `neon_cyberpunk` | Dark with electric pink/cyan |
| `warm_beige` | Vintage sepia tones |
| `pastel_dream` | Soft muted pastels |
| `japanese_ink` | Minimalist ink wash style |
| `forest` | Deep greens and sage |
| `ocean` | Blues and teals for coastal cities |
| `terracotta` | Mediterranean warmth |
| `sunset` | Warm oranges and pinks |
| `autumn` | Seasonal burnt oranges and reds |
| `copper_patina` | Oxidized copper aesthetic |
| `monochrome_blue` | Single blue color family |

## 输出

Posters are saved to `posters/` directory with format:

```text
{city}_{theme}_{YYYYMMDD_HHMMSS}.png
```

## 添加自定义主题

Create a JSON file in `themes/` directory:

```json
{
  "name": "My Theme",
  "description": "Description of the theme",
  "bg": "#FFFFFF",
  "text": "#000000",
  "gradient_color": "#FFFFFF",
  "water": "#C0C0C0",
  "parks": "#F0F0F0",
  "road_motorway": "#0A0A0A",
  "road_primary": "#1A1A1A",
  "road_secondary": "#2A2A2A",
  "road_tertiary": "#3A3A3A",
  "road_residential": "#4A4A4A",
  "road_default": "#3A3A3A"
}
```

## 项目结构

```text
map_poster/
├── create_map_poster.py    # Main script
├── font_management.py      # Font loading and Google Fonts integration
├── themes/                 # Theme JSON files
├── fonts/                  # Font files
│   ├── Roboto-*.ttf        # Default Roboto fonts
│   └── cache/              # Downloaded Google Fonts (auto-generated)
├── posters/                # Generated posters
└── README.md
```


## 黑客指南

供希望扩展或修改脚本的贡献者快速参考。

### 贡献者指南

- 欢迎 bug 修复
- 不要提交用户界面（Web/桌面）
- 暂时不要 Docker 化
- 如果您修复了任何代码，请测试并查看修复前后的海报版本
- 在开始开发大型功能之前，请在 Discussions/Issue 中询问是否会被合并

### 架构概述

```text
┌─────────────────┐     ┌──────────────┐     ┌─────────────────┐
│   CLI Parser    │────▶│  Geocoding   │────▶│  Data Fetching  │
│   (argparse)    │     │  (Nominatim) │     │    (OSMnx)      │
└─────────────────┘     └──────────────┘     └─────────────────┘
                                                     │
                        ┌──────────────┐             ▼
                        │    Output    │◀────┌─────────────────┐
                        │  (matplotlib)│     │   Rendering     │
                        └──────────────┘     │  (matplotlib)   │
                                             └─────────────────┘
```

### Key Functions

| Function | Purpose | Modify when... |
|----------|---------|----------------|
| `get_coordinates()` | City → lat/lon via Nominatim | Switching geocoding provider |
| `create_poster()` | Main rendering pipeline | Adding new map layers |
| `get_edge_colors_by_type()` | Road color by OSM highway tag | Changing road styling |
| `get_edge_widths_by_type()` | Road width by importance | Adjusting line weights |
| `create_gradient_fade()` | Top/bottom fade effect | Modifying gradient overlay |
| `load_theme()` | JSON theme → dict | Adding new theme properties |
| `is_latin_script()` | Detects script for typography | Supporting new scripts |
| `load_fonts()` | Load custom/default fonts | Changing font loading logic |

### Rendering Layers (z-order)

```text
z=11  Text labels (city, country, coords)
z=10  Gradient fades (top & bottom)
z=3   Roads (via ox.plot_graph)
z=2   Parks (green polygons)
z=1   Water (blue polygons)
z=0   Background color
```

### OSM Highway Types → Road Hierarchy

```python
# In get_edge_colors_by_type() and get_edge_widths_by_type()
motorway, motorway_link     → Thickest (1.2), darkest
trunk, primary              → Thick (1.0)
secondary                   → Medium (0.8)
tertiary                    → Thin (0.6)
residential, living_street  → Thinnest (0.4), lightest
```

### Typography & Script Detection

The script automatically detects text scripts to apply appropriate typography:

- **Latin scripts** (English, French, Spanish, etc.): Letter spacing applied for elegant "P  A  R  I  S" effect
- **Non-Latin scripts** (Japanese, Arabic, Thai, Korean, etc.): Natural spacing for "東京" (no gaps between characters)

Script detection uses Unicode ranges (U+0000-U+024F for Latin). If >80% of alphabetic characters are Latin, spacing is applied.

### Adding New Features

**New map layer (e.g., railways):**

```python
# In create_poster(), after parks fetch:
try:
    railways = ox.features_from_point(point, tags={'railway': 'rail'}, dist=dist)
except:
    railways = None

# Then plot before roads:
if railways is not None and not railways.empty:
    railways.plot(ax=ax, color=THEME['railway'], linewidth=0.5, zorder=2.5)
```

**New theme property:**

1. Add to theme JSON: `"railway": "#FF0000"`
2. Use in code: `THEME['railway']`
3. Add fallback in `load_theme()` default dict

### Typography Positioning

All text uses `transform=ax.transAxes` (0-1 normalized coordinates):

```text
y=0.14  City name (spaced letters for Latin scripts)
y=0.125 Decorative line
y=0.10  Country name
y=0.07  Coordinates
y=0.02  Attribution (bottom-right)
```

### Useful OSMnx Patterns

```python
# Get all buildings
buildings = ox.features_from_point(point, tags={'building': True}, dist=dist)

# Get specific amenities
cafes = ox.features_from_point(point, tags={'amenity': 'cafe'}, dist=dist)

# Different network types
G = ox.graph_from_point(point, dist=dist, network_type='drive')  # roads only
G = ox.graph_from_point(point, dist=dist, network_type='bike')   # bike paths
G = ox.graph_from_point(point, dist=dist, network_type='walk')   # pedestrian
```

### Performance Tips

- Large `dist` values (>20km) = slow downloads + memory heavy
- Cache coordinates locally to avoid Nominatim rate limits
- Use `network_type='drive'` instead of `'all'` for faster renders
- Reduce `dpi` from 300 to 150 for quick previews
