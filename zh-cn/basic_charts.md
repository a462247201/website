## Calendar：日历图

> *class pyecharts.charts.Calendar*

```python
class Calendar(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyeachrts.charts.Calendar.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据，格式为 [(date1, value1), (date2, value2), ...]
    yaxis_data: Sequence,

    # 是否选中图例
    is_selected: bool = True,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 日历坐标系组件配置项，参考 `CalendarOpts`
    calendar_opts: Union[opts.CalendarOpts, dict, None] = None,

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 图元样式配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

### CalendarOpts：日历坐标系组件配置项

> *class pyecharts.options.CalendarOpts*

```python
class CalendarOpts(
    # calendar组件离容器左侧的距离。
    # left 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比，
    # 也可以是 'left', 'center', 'right'。
    # 如果 left 的值为'left', 'center', 'right'，组件会根据相应的位置自动对齐。
    pos_left: Optional[str] = None,

    # calendar组件离容器上侧的距离。
    # top 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比，
    # 也可以是 'top', 'middle', 'bottom'。
    # 如果 top 的值为'top', 'middle', 'bottom'，组件会根据相应的位置自动对齐。
    pos_top: Optional[str] = None,

    # calendar组件离容器右侧的距离。
    # right 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比。
    # 默认自适应。
    pos_right: Optional[str] = None,

    # calendar组件离容器下侧的距离。
    # bottom 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比。
    # 默认自适应。
    pos_bottom: Optional[str] = None,

    # 日历坐标的布局朝向。可选：
    # 'horizontal', 'vertical'
    orient: Optional[str] = None,
    # 必填，日历坐标的范围 支持多种格式，使用示例：
    # 某一年 range: 2017
    # 某个月 range: '2017-02'
    # 某个区间 range: ['2017-01-02', '2017-02-23']
    # 注意 此写法会识别为['2017-01-01', '2017-02-01']
    # range: ['2017-01', '2017-02']
    range_: Union[str, Sequence, int] = None,

    # 星期轴的样式，参考 `series_options.LabelOpts`
    daylabel_opts: Union[LabelOpts, dict, None] = None,

    # 月份轴的样式，参考 `series_options.LabelOpts`
    monthlabel_opts: Union[LabelOpts, dict, None] = None,

    # 年份的样式，参考 `series_options.LabelOpts`
    yearlabel_opts: Union[LabelOpts, dict, None] = None,
)
```

### Demo

> Calendar-2017年微信步数情况

```python
import datetime
import random

from pyecharts import options as opts
from pyecharts.charts import Calendar


def calendar_base() -> Calendar:
    begin = datetime.date(2017, 1, 1)
    end = datetime.date(2017, 12, 31)
    data = [
        [str(begin + datetime.timedelta(days=i)), random.randint(1000, 25000)]
        for i in range((end - begin).days + 1)
    ]

    c = (
        Calendar()
        .add("", data, calendar_opts=opts.CalendarOpts(range_="2017"))
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Calendar-2017年微信步数情况"),
            visualmap_opts=opts.VisualMapOpts(
                max_=20000,
                min_=500,
                orient="horizontal",
                is_piecewise=True,
                pos_top="230px",
                pos_left="100px",
            ),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55605195-f7324d00-57a5-11e9-8b1c-1042e60e0431.png)


## Funnel：漏斗图

> *class pyecharts.charts.Funnel*

```python
class Funnel(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Funnel.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据项，格式为 [(key1, value1), (key2, value2)]
    data_pair: Sequence,

    # 是否选中图例
    is_selected: bool = True,

    # 系列 label 颜色
    color: Optional[str] = None,

    # 数据排序， 可以取 'ascending'，'descending'，'none'（表示按 data 顺序）
    sort_: str = "descending",

    # 数据图形间距
    gap: Numeric = 0,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 图元样式配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

### Demo

> Funnel-基本示例

```python
from pyecharts.faker import Faker
from pyecharts import options as opts
from pyecharts.charts import Funnel, Page


def funnel_base() -> Funnel:
    c = (
        Funnel()
        .add("商品", [list(z) for z in zip(Faker.choose(), Faker.values())])
        .set_global_opts(title_opts=opts.TitleOpts(title="Funnel-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55929585-fb4fe600-5c4f-11e9-8c31-60edd9c8b2b9.png)

> Funnel-Label（inside)

```python
def funnel_label_inside() -> Funnel:
    c = (
        Funnel()
        .add(
            "商品",
            [list(z) for z in zip(Faker.choose(), Faker.values())],
            label_opts=opts.LabelOpts(position="inside"),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Funnel-Label（inside)"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55929620-191d4b00-5c50-11e9-97eb-b6ea184d1140.png)

> Funnel-Sort（ascending）

```python
def funnel_sort_ascending() -> Funnel:
    c = (
        Funnel()
        .add(
            "商品",
            [list(z) for z in zip(Faker.choose(), Faker.values())],
            sort_="ascending",
            label_opts=opts.LabelOpts(position="inside"),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Funnel-Sort（ascending）"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55929629-233f4980-5c50-11e9-8dbe-9562b3fdfdd5.png)


## Gauge：仪表盘

> *class pyecharts.charts.Gauge*

```python
class Gauge(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Gauge.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据项，格式为 [(key1, value1), (key2, value2)]
    data_pair: Sequence,

    # 是否选中图例
    is_selected: bool = True,

    # 最小的数据值
    min_: Numeric = 0,

    # 最大的数据值
    max_: Numeric = 100,

    # 仪表盘平均分割段数
    split_number: Numeric = 10,

    # 仪表盘半径，可以是相对于容器高宽中较小的一项的一半的百分比，也可以是绝对的数值。
    radius: types.Union[types.Numeric, str] = "75%",

    # 仪表盘起始角度。圆心 正右手侧为0度，正上方为 90 度，正左手侧为 180 度。
    start_angle: Numeric = 225,

    # 仪表盘结束角度。
    end_angle: Numeric = -45,
    
    # 轮盘内标题文本项标签配置项，参考 `series_options.LabelOpts`
    title_label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 轮盘内数据项标签配置项，参考 `series_options.LabelOpts`
    detail_label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 图元样式配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

### Demo

> Gauge-基本示例

```python
from pyecharts import options as opts
from pyecharts.charts import Gauge, Page


def gauge_base() -> Gauge:
    c = (
        Gauge()
        .add("", [("完成率", 66.6)])
        .set_global_opts(title_opts=opts.TitleOpts(title="Gauge-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55929665-3ce09100-5c50-11e9-8bba-9156fdbde06b.png)

> Gauge-不同颜色

```python
def gauge_color() -> Gauge:
    c = (
        Gauge()
        .add(
            "业务指标",
            [("完成率", 55.5)],
            axisline_opts=opts.AxisLineOpts(
                linestyle_opts=opts.LineStyleOpts(
                    color=[(0.3, "#67e0e3"), (0.7, "#37a2da"), (1, "#fd666d")], width=30
                )
            ),
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Gauge-不同颜色"),
            legend_opts=opts.LegendOpts(is_show=False),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/56973361-48640f80-6b9f-11e9-9196-5e1147e3ac91.png)

> Gauge-分割段数-Label

```python
def gauge_splitnum_label() -> Gauge:
    c = (
        Gauge()
        .add(
            "业务指标",
            [("完成率", 55.5)],
            split_number=5,
            axisline_opts=opts.AxisLineOpts(
                linestyle_opts=opts.LineStyleOpts(
                    color=[(0.3, "#67e0e3"), (0.7, "#37a2da"), (1, "#fd666d")], width=30
                )
            ),
            label_opts=opts.LabelOpts(formatter="{value}"),
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Gauge-分割段数-Label"),
            legend_opts=opts.LegendOpts(is_show=False),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/58701514-bb96b680-83d5-11e9-8460-e5b0c4a39c0c.png)

> Gauge-改变轮盘内的字体

```python
def gauge_label_title_setting() -> Gauge:
    c = (
        Gauge()
        .add(
            "",
            [("完成率", 66.6)],
            title_label_opts=opts.LabelOpts(
                font_size=40, color="blue", font_family="Microsoft YaHei"
            ),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Gauge-改变轮盘内的字体"))
    )
    return c
```
![](https://user-images.githubusercontent.com/17564655/66656043-c90b5980-ec6f-11e9-91f2-106010e35864.png)


## Graph：关系图

> *class pyecharts.charts.Graph*

```python
class Graph(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *class pyecharts.charts.Graph.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 关系图节点数据项列表，参考 `opts.GraphNode`
    nodes: Sequence[Union[opts.GraphNode, dict]],

    # 关系图节点间关系数据项列表，参考 `opts.GraphLink`
    links: Sequence[Union[opts.GraphLink, dict]],

    # 关系图节点分类的类目列表，参考 `opts.GraphCategory`
    categories: Union[Sequence[Union[opts.GraphCategory, dict]], None] = None,

    # 是否选中图例。
    is_selected: bool = True,

    # 是否在鼠标移到节点上的时候突出显示节点以及节点的边和邻接节点。
    is_focusnode: bool = True,

    # 是否开启鼠标缩放和平移漫游。
    is_roam: bool = True,
    
    # 节点是否可拖拽，只在使用力引导布局的时候有用。
    is_draggable: bool = False,

    # 是否旋转标签，默认不旋转。
    is_rotate_label: bool = False,

    # 图的布局。可选：
    # 'none' 不采用任何布局，使用节点中提供的 x， y 作为节点的位置。
    # 'circular' 采用环形布局。
    # 'force' 采用力引导布局。
    layout: str = "force",

    # 关系图节点标记的图形。
    # ECharts 提供的标记类型包括 'circle', 'rect', 'roundRect', 'triangle', 
    # 'diamond', 'pin', 'arrow', 'none'
    # 可以通过 'image://url' 设置为图片，其中 URL 为图片的链接，或者 dataURI。
    symbol: Optional[str] = None,
    
    # 关系图节点标记的大小
    # 可以设置成诸如 10 这样单一的数字
    # 也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbol_size: types.Numeric = 10,

    # 边的两个节点之间的距离，这个距离也会受 repulsion。
    # 支持设置成数组表达边长的范围，此时不同大小的值会线性映射到不同的长度。值越小则长度越长。
    edge_length: Numeric = 50,

    # 节点受到的向中心的引力因子。该值越大节点越往中心点靠拢。
    gravity: Numeric = 0.2,

    # 节点之间的斥力因子。
    # 支持设置成数组表达斥力的范围，此时不同大小的值会线性映射到不同的斥力。值越大则斥力越大
    repulsion: Numeric = 50,

     # Graph 图节点边的 Label 配置（即在边上显示数据或标注的配置）
    edge_label: types.Label = None,

    # 边两端的标记类型，可以是一个数组分别指定两端，也可以是单个统一指定。
    # 默认不显示标记，常见的可以设置为箭头，如下：edgeSymbol: ['circle', 'arrow']
    edge_symbol: Optional[str] = None,
    
    # 边两端的标记大小，可以是一个数组分别指定两端，也可以是单个统一指定。
    edge_symbol_size: Numeric = 10,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 关系边的公用线条样式。
    linestyle_opts: Union[opts.LineStyleOpts, dict] = opts.LineStyleOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 图元样式配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

### GraphNode：关系图的节点数据项

> *class pyecharts.options.GraphNode*

```python
class GraphNode(
    # 数据项名称。
    name: Optional[str] = None,

    # 节点的初始 x 值。在不指定的时候需要指明layout属性选择布局方式。
    x: Optional[Numeric] = None,

    # 节点的初始 y 值。在不指定的时候需要指明layout属性选择布局方式。
    y: Optional[Numeric] = None,

    # 节点在力引导布局中是否固定。
    is_fixed: bool = False,

    # 数据项值。
    value: Union[str, Sequence, None] = None,

    # 数据项所在类目的 index。
    category: Optional[int] = None,

    # 该类目节点标记的图形。
    # ECharts 提供的标记类型包括 'circle', 'rect', 'roundRect', 'triangle', 
    # 'diamond', 'pin', 'arrow', 'none'
    # 可以通过 'image://url' 设置为图片，其中 URL 为图片的链接，或者 dataURI。
    symbol: Optional[str] = None,

    # 该类目节点标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，
    # 例如 [20, 10] 表示标记宽为 20，高为 10。
    symbol_size: Union[Numeric, Sequence, None] = None,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Optional[LabelOpts] = None,
)
```

### GraphLink：节点间的关系数据

> *class pyecharts.options.GraphLink*

```python
class GraphLink(
    # 边的源节点名称的字符串，也支持使用数字表示源节点的索引。
    source: Union[str, int, None] = None,

    # 边的目标节点名称的字符串，也支持使用数字表示源节点的索引。
    target: Union[str, int, None] = None,

    # 边的数值，可以在力引导布局中用于映射到边的长度。
    value: Optional[Numeric] = None,

    # 边两端的标记类型，可以是一个数组分别指定两端，也可以是单个统一指定。
    symbol: Union[str, Sequence, None] = None,

    # 边两端的标记大小，可以是一个数组分别指定两端，也可以是单个统一指定。
    symbol_size: Union[Numeric, Sequence, None] = None,

    # 关系边的线条样式，参考 `series_options.LineStyleOpts`
    linestyle_opts: Optional[LineStyleOpts] = None,

    # 标签样式，参考 `series_options.LabelOpts`
    label_opts: Optional[LabelOpts] = None,
)
```

### GraphCategory：节点分类的类目

> *class pyecharts.options.GraphCategory*

```python
class GraphCategory(
    # 类目名称，用于和 legend 对应以及格式化 tooltip 的内容。
    name: Optional[str] = None,

    # 该类目节点标记的图形。
    # ECharts 提供的标记类型包括 'circle', 'rect', 'roundRect', 'triangle', 
    # 'diamond', 'pin', 'arrow', 'none'
    # 可以通过 'image://url' 设置为图片，其中 URL 为图片的链接，或者 dataURI。
    symbol: Optional[str] = None,

    # 该类目节点标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，
    # 例如 [20, 10] 表示标记宽为 20，高为 10。
    symbol_size: Union[Numeric, Sequence, None] = None,

    # # 标签样式，参考 `series_options.LabelOpts`
    label_opts: Optional[LabelOpts] = None,
)
```

### Demo

> Graph-基本示例

```python
import json
import os

from pyecharts import options as opts
from pyecharts.charts import Graph, Page


def graph_base() -> Graph:
    nodes = [
        {"name": "结点1", "symbolSize": 10},
        {"name": "结点2", "symbolSize": 20},
        {"name": "结点3", "symbolSize": 30},
        {"name": "结点4", "symbolSize": 40},
        {"name": "结点5", "symbolSize": 50},
        {"name": "结点6", "symbolSize": 40},
        {"name": "结点7", "symbolSize": 30},
        {"name": "结点8", "symbolSize": 20},
    ]
    links = []
    for i in nodes:
        for j in nodes:
            links.append({"source": i.get("name"), "target": j.get("name")})
    c = (
        Graph()
        .add("", nodes, links, repulsion=8000)
        .set_global_opts(title_opts=opts.TitleOpts(title="Graph-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931719-37d40f80-5c59-11e9-9f1f-86326f4250f2.png)

> Graph-GraphNode-GraphLink

```python
def graph_with_opts() -> Graph:
    nodes = [
        opts.GraphNode(name="结点1", symbol_size=10),
        opts.GraphNode(name="结点2", symbol_size=20),
        opts.GraphNode(name="结点3", symbol_size=30),
        opts.GraphNode(name="结点4", symbol_size=40),
        opts.GraphNode(name="结点5", symbol_size=50),
    ]
    links = [
        opts.GraphLink(source="结点1", target="结点2"),
        opts.GraphLink(source="结点2", target="结点3"),
        opts.GraphLink(source="结点3", target="结点4"),
        opts.GraphLink(source="结点4", target="结点5"),
        opts.GraphLink(source="结点5", target="结点1"),
    ]
    c = (
        Graph()
        .add("", nodes, links, repulsion=4000)
        .set_global_opts(title_opts=opts.TitleOpts(title="Graph-GraphNode-GraphLink"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931745-47535880-5c59-11e9-8728-9216afd2975b.png)

> Graph-GraphNode-GraphLink-WithEdgeLabel

```python
def graph_with_edge_opts() -> Graph:
    nodes_data = [
        opts.GraphNode(name="结点1", symbol_size=10),
        opts.GraphNode(name="结点2", symbol_size=20),
        opts.GraphNode(name="结点3", symbol_size=30),
        opts.GraphNode(name="结点4", symbol_size=40),
        opts.GraphNode(name="结点5", symbol_size=50),
        opts.GraphNode(name="结点6", symbol_size=60),
    ]
    links_data = [
        opts.GraphLink(source="结点1", target="结点2", value=2),
        opts.GraphLink(source="结点2", target="结点3", value=3),
        opts.GraphLink(source="结点3", target="结点4", value=4),
        opts.GraphLink(source="结点4", target="结点5", value=5),
        opts.GraphLink(source="结点5", target="结点6", value=6),
        opts.GraphLink(source="结点6", target="结点1", value=7),
    ]
    c = (
        Graph()
        .add(
            "",
            nodes_data,
            links_data,
            repulsion=4000,
            edge_label=opts.LabelOpts(
                is_show=True,
                position="middle",
                formatter="{b} 的数据 {c}",
            ),
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Graph-GraphNode-GraphLink-WithEdgeLabel")
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/17564655/71709673-9b2f4e80-2e33-11ea-977e-60d7f0b5b01a.png)

> Graph-微博转发关系图

```python
def graph_weibo() -> Graph:
    with open(os.path.join("fixtures", "weibo.json"), "r", encoding="utf-8") as f:
        j = json.load(f)
        nodes, links, categories, cont, mid, userl = j
    c = (
        Graph()
        .add(
            "",
            nodes,
            links,
            categories,
            repulsion=50,
            linestyle_opts=opts.LineStyleOpts(curve=0.2),
            label_opts=opts.LabelOpts(is_show=False),
        )
        .set_global_opts(
            legend_opts=opts.LegendOpts(is_show=False),
            title_opts=opts.TitleOpts(title="Graph-微博转发关系图"),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931763-5b975580-5c59-11e9-966c-b54705924b88.png)

> Graph-les-miserables

```python
def graph_les_miserables():
    with open(
        os.path.join("fixtures", "les-miserables.json"), "r", encoding="utf-8"
    ) as f:
        j = json.load(f)
        nodes = j["nodes"]
        links = j["links"]
        categories = j["categories"]

    c = (
        Graph(init_opts=opts.InitOpts(width="1000px", height="600px"))
        .add(
            "",
            nodes=nodes,
            links=links,
            categories=categories,
            layout="circular",
            is_rotate_label=True,
            linestyle_opts=opts.LineStyleOpts(color="source", curve=0.3),
            label_opts=opts.LabelOpts(position="right"),
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Graph-Les Miserables"),
            legend_opts=opts.LegendOpts(
                orient="vertical", pos_left="2%", pos_top="20%"
            ),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/62337103-cd93f300-b505-11e9-9bfd-165d4d1a870c.png)

> Graph-NPM Dependencies

```python
def graph_npm_dependencies() -> Graph:
    with open(os.path.join("fixtures", "npmdepgraph.json"), "r", encoding="utf-8") as f:
        j = json.load(f)
    nodes = [
        {
            "x": node["x"],
            "y": node["y"],
            "id": node["id"],
            "name": node["label"],
            "symbolSize": node["size"],
            "itemStyle": {"normal": {"color": node["color"]}},
        }
        for node in j["nodes"]
    ]

    edges = [
        {"source": edge["sourceID"], "target": edge["targetID"]} for edge in j["edges"]
    ]

    c = (
        Graph(init_opts=opts.InitOpts(width="1000px", height="600px"))
        .add(
            "",
            nodes=nodes,
            links=edges,
            layout="none",
            label_opts=opts.LabelOpts(is_show=False),
            linestyle_opts=opts.LineStyleOpts(width=0.5, curve=0.3, opacity=0.7),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Graph-NPM Dependencies"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/57499076-e29b2480-7310-11e9-85db-29712819308d.png)


## Liquid：水球图

> *class pyecharts.charts.Liquid*

```python
class Liquid(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Liquid.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据，格式为 [value1, value2, ....]
    data: Sequence,

    # 水球外形，有' circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow' 可选。
    # 默认 'circle'。也可以为自定义的 SVG 路径。
    shape: str = "circle",

    # 波浪颜色。
    color: Optional[Sequence[str]] = None,

    # 是否显示波浪动画。
    is_animation: bool = True,

    # 是否显示边框。
    is_outline_show: bool = True,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(font_size=50, position="inside"),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,
)
```

### Demo

> Liquid-基本示例

```python
from pyecharts import options as opts
from pyecharts.charts import Liquid, Page
from pyecharts.globals import SymbolType


def liquid_base() -> Liquid:
    c = (
        Liquid()
        .add("lq", [0.6, 0.7])
        .set_global_opts(title_opts=opts.TitleOpts(title="Liquid-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931845-aadd8600-5c59-11e9-9446-7700ddb3e875.gif)

> Liquid-数据精度

```python
def liquid_data_precision() -> Liquid:
    c = (
        Liquid()
        .add(
            "lq",
            [0.3254],
            label_opts=opts.LabelOpts(
                font_size=50,
                formatter=JsCode(
                    """function (param) {
                        return (Math.floor(param.value * 10000) / 100) + '%';
                    }"""
                ),
                position="inside",
            ),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Liquid-数据精度"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/57499126-0a8a8800-7311-11e9-8d05-0040c5a70de4.png)

> Liquid-无边框

```python
def liquid_without_outline() -> Liquid:
    c = (
        Liquid()
        .add("lq", [0.6, 0.7, 0.8], is_outline_show=False)
        .set_global_opts(title_opts=opts.TitleOpts(title="Liquid-无边框"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931903-e710e680-5c59-11e9-9d34-1eab6fdc22b5.png)

> Liquid-Shape-diamond

```python
def liquid_shape_diamond() -> Liquid:
    c = (
        Liquid()
        .add("lq", [0.4, 0.7], is_outline_show=False, shape=SymbolType.DIAMOND)
        .set_global_opts(title_opts=opts.TitleOpts(title="Liquid-Shape-diamond"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931921-f1cb7b80-5c59-11e9-916c-75db9bad367d.png)

> Liquid-Shape-arrow

```python
def liquid_shape_arrow() -> Liquid:
    c = (
        Liquid()
        .add("lq", [0.3, 0.7], is_outline_show=False, shape=SymbolType.ARROW)
        .set_global_opts(title_opts=opts.TitleOpts(title="Liquid-Shape-arrow"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931932-027bf180-5c5a-11e9-8ed5-f55c43ce58fc.png)

> Liquid-Shape-rect

```python
def liquid_shape_rect() -> Liquid:
    c = (
        Liquid()
        .add("lq", [0.3, 0.7], is_outline_show=False, shape=SymbolType.RECT)
        .set_global_opts(title_opts=opts.TitleOpts(title="Liquid-Shape-rect"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55931939-0e67b380-5c5a-11e9-9986-bc7bfe3adc43.png)


## Parallel：平行坐标系

> *class pyecharts.charts.Parallel*

```python
class Parallel(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Parallel.add_schema*

```python
def add_schema(
    schema: Sequence[Union[opts.ParallelAxisOpts, dict]],
    parallel_opts: Union[opts.ParallelOpts, dict, None] = None,
)
```

> *func pyecharts.charts.Parallel.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据
    data: Sequence,

    # 是否选中图例。
    is_selected: bool = True,

    # 是否平滑曲线
    is_smooth: bool = False,

    # 线条样式，参考 `series_options.LineStyleOpts`
    linestyle_opts: Union[opts.LineStyleOpts, dict] = opts.LineStyleOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 图元样式配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

### ParallelOpts：平行坐标系配置项

> *class pyecharts.options.ParallelOpts*

```python
class ParallelOpts(
    # parallel 组件离容器左侧的距离。
    # left 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比，
    # 也可以是 'left', 'center', 'right'。
    # 如果 left 的值为'left', 'center', 'right'，组件会根据相应的位置自动对齐。
    pos_left: str = "5%",

    # parallel 组件离容器右侧的距离。
    # right 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比。
    pos_right: str = "13%",

    # parallel 组件离容器下侧的距离。
    # bottom 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比。
    pos_bottom: str = "10%",

    # parallel 组件离容器上侧的距离。
    # top 的值可以是像 20 这样的具体像素值，可以是像 '20%' 这样相对于容器高宽的百分比，
    # 也可以是 'top', 'middle', 'bottom'。
    # 如果 top 的值为'top', 'middle', 'bottom'，组件会根据相应的位置自动对齐。
    pos_top: str = "20%",

    # 布局方式，可选值为：
    # 'horizontal'：水平排布各个坐标轴。
    # 'vertical'：竖直排布各个坐标轴。
    layout: Optional[str] = None,
)
```

### ParallelAxisOpts：平行坐标系轴配置项

> *class pyecharts.options.ParallelAxisOpts*

```python
class ParallelAxisOpts(
    # 坐标轴的维度序号。
    dim: Numeric,

    # 坐标轴名称。
    name: str,

    # 坐标轴数据项
    data: Sequence = None,

    # 坐标轴类型。可选：
    # 'value': 数值轴，适用于连续数据。
    # 'category': 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
    # 'time': 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同
    # 例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。
    # 'log' 对数轴。适用于对数数据。
    type_: Optional[str] = None,

    # 坐标轴刻度最小值。
    # 可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。
    # 不设置时会自动计算最小值保证坐标轴刻度的均匀分布。
    # 在类目轴中，也可以设置为类目的序数（如类目轴 data: ['类A', '类B', '类C'] 中，序数 2 表示 '类C'
    # 也可以设置为负数，如 -3）。
    min_: Union[str, Numeric, None] = None,

    # 坐标轴刻度最大值。
    # 可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。
    # 不设置时会自动计算最大值保证坐标轴刻度的均匀分布。
    # 在类目轴中，也可以设置为类目的序数（如类目轴 data: ['类A', '类B', '类C'] 中，序数 2 表示 '类C'
    # 也可以设置为负数，如 -3）。
    max_: Union[str, Numeric, None] = None,

    # 只在数值轴中（type: 'value'）有效。
    # 是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。
    # 在设置 min 和 max 之后该配置项无效。
    is_scale: bool = False,
)
```

### Demo

> Parallel-基本示例

```python
from pyecharts import options as opts
from pyecharts.charts import Page, Parallel


def parallel_base() -> Parallel:
    data = [
        [1, 91, 45, 125, 0.82, 34],
        [2, 65, 27, 78, 0.86, 45],
        [3, 83, 60, 84, 1.09, 73],
        [4, 109, 81, 121, 1.28, 68],
        [5, 106, 77, 114, 1.07, 55],
        [6, 109, 81, 121, 1.28, 68],
        [7, 106, 77, 114, 1.07, 55],
        [8, 89, 65, 78, 0.86, 51, 26],
        [9, 53, 33, 47, 0.64, 50, 17],
        [10, 80, 55, 80, 1.01, 75, 24],
        [11, 117, 81, 124, 1.03, 45],
    ]
    c = (
        Parallel()
        .add_schema(
            [
                {"dim": 0, "name": "data"},
                {"dim": 1, "name": "AQI"},
                {"dim": 2, "name": "PM2.5"},
                {"dim": 3, "name": "PM10"},
                {"dim": 4, "name": "CO"},
                {"dim": 5, "name": "NO2"},
            ]
        )
        .add("parallel", data)
        .set_global_opts(title_opts=opts.TitleOpts(title="Parallel-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55932922-24777300-5c5e-11e9-80f5-6af49727ef11.png)

> Parallel-Category

```python
def parallel_category() -> Parallel:
    data = [
        [1, 91, 45, 125, 0.82, 34, 23, "良"],
        [2, 65, 27, 78, 0.86, 45, 29, "良"],
        [3, 83, 60, 84, 1.09, 73, 27, "良"],
        [4, 109, 81, 121, 1.28, 68, 51, "轻度污染"],
        [5, 106, 77, 114, 1.07, 55, 51, "轻度污染"],
        [6, 109, 81, 121, 1.28, 68, 51, "轻度污染"],
        [7, 106, 77, 114, 1.07, 55, 51, "轻度污染"],
        [8, 89, 65, 78, 0.86, 51, 26, "良"],
        [9, 53, 33, 47, 0.64, 50, 17, "良"],
        [10, 80, 55, 80, 1.01, 75, 24, "良"],
        [11, 117, 81, 124, 1.03, 45, 24, "轻度污染"],
        [12, 99, 71, 142, 1.1, 62, 42, "良"],
        [13, 95, 69, 130, 1.28, 74, 50, "良"],
        [14, 116, 87, 131, 1.47, 84, 40, "轻度污染"],
    ]
    c = (
        Parallel()
        .add_schema(
            [
                opts.ParallelAxisOpts(dim=0, name="data"),
                opts.ParallelAxisOpts(dim=1, name="AQI"),
                opts.ParallelAxisOpts(dim=2, name="PM2.5"),
                opts.ParallelAxisOpts(dim=3, name="PM10"),
                opts.ParallelAxisOpts(dim=4, name="CO"),
                opts.ParallelAxisOpts(dim=5, name="NO2"),
                opts.ParallelAxisOpts(dim=6, name="CO2"),
                opts.ParallelAxisOpts(
                    dim=7,
                    name="等级",
                    type_="category",
                    data=["优", "良", "轻度污染", "中度污染", "重度污染", "严重污染"],
                ),
            ]
        )
        .add("parallel", data)
        .set_global_opts(title_opts=opts.TitleOpts(title="Parallel-Category"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55932940-2fca9e80-5c5e-11e9-9a36-78882da3ff78.png)


## Pie：饼图

> *class pyecharts.charts.Pie*

```python
class Pie(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Pie.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据项，格式为 [(key1, value1), (key2, value2)]
    data_pair: Sequence,

    # 系列 label 颜色
    color: Optional[str] = None,

    # 饼图的半径，数组的第一项是内半径，第二项是外半径
    # 默认设置成百分比，相对于容器高宽中较小的一项的一半
    radius: Optional[Sequence] = None,

    # 饼图的中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标
    # 默认设置成百分比，设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度
    center: Optional[Sequence] = None,

    # 是否展示成南丁格尔图，通过半径区分数据大小，有'radius'和'area'两种模式。
    # radius：扇区圆心角展现数据的百分比，半径展现数据的大小
    # area：所有扇区圆心角相同，仅通过半径展现数据大小
    rosetype: Optional[str] = None,
    
    # 饼图的扇区是否是顺时针排布。
    is_clockwise: bool = True,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 图元样式配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

### Demo

> Pie-基本示例

```python
from pyecharts.faker import Faker
from pyecharts import options as opts
from pyecharts.charts import Pie


def pie_base() -> Pie:
    c = (
        Pie()
        .add("", [list(z) for z in zip(Faker.choose(), Faker.values())])
        .set_global_opts(title_opts=opts.TitleOpts(title="Pie-基本示例"))
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933061-9354cc00-5c5e-11e9-8f80-5e2f434a1ec4.png)

> Pie-设置颜色

```python
def pie_set_colors() -> Pie:
    c = (
        Pie()
        .add("", [list(z) for z in zip(Faker.choose(), Faker.values())])
        .set_colors(["blue", "green", "yellow", "red", "pink", "orange", "purple"])
        .set_global_opts(title_opts=opts.TitleOpts(title="Pie-设置颜色"))
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/58471056-96a40880-8175-11e9-835c-a9ac8c4fc784.png)

> Pie-调整位置

```python
def pie_position() -> Pie:
    c = (
        Pie()
        .add(
            "",
            [list(z) for z in zip(Faker.choose(), Faker.values())],
            center=["35%", "50%"],
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Pie-调整位置"),
            legend_opts=opts.LegendOpts(pos_left="15%"),
        )
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/57317851-a5297200-712b-11e9-9f06-b46698ed42cc.png)

> Pie-Radius

```python
def pie_radius() -> Pie:
    c = (
        Pie()
        .add(
            "",
            [list(z) for z in zip(Faker.choose(), Faker.values())],
            radius=["40%", "75%"],
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Pie-Radius"),
            legend_opts=opts.LegendOpts(
                orient="vertical", pos_top="15%", pos_left="2%"
            ),
        )
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933080-a9fb2300-5c5e-11e9-9be2-61e806577b69.png)

> Pie-玫瑰图示例

```python
def pie_rosetype() -> Pie:
    v = Faker.choose()
    c = (
        Pie()
        .add(
            "",
            [list(z) for z in zip(v, Faker.values())],
            radius=["30%", "75%"],
            center=["25%", "50%"],
            rosetype="radius",
            label_opts=opts.LabelOpts(is_show=False),
        )
        .add(
            "",
            [list(z) for z in zip(v, Faker.values())],
            radius=["30%", "75%"],
            center=["75%", "50%"],
            rosetype="area",
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Pie-玫瑰图示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933111-b4b5b800-5c5e-11e9-9dad-3aaa7870d858.png)

> Pie-Legend 滚动

```python
def pie_scroll_legend() -> Pie:
    c = (
        Pie()
        .add(
            "",
            [
                list(z)
                for z in zip(
                    Faker.choose() + Faker.choose() + Faker.choose(),
                    Faker.values() + Faker.values() + Faker.values(),
                )
            ],
            center=["40%", "50%"],
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Pie-Legend 滚动"),
            legend_opts=opts.LegendOpts(
                type_="scroll", pos_left="80%", orient="vertical"
            ),
        )
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/58844718-0dc42a00-86ab-11e9-9a1d-93279046dde2.png)

> Pie-富文本示例

```python
def pie_rich_label() -> Pie:
    c = (
        Pie()
        .add(
            "",
            [list(z) for z in zip(Faker.choose(), Faker.values())],
            radius=["40%", "55%"],
            label_opts=opts.LabelOpts(
                position="outside",
                formatter="{a|{a}}{abg|}\n{hr|}\n {b|{b}: }{c}  {per|{d}%}  ",
                background_color="#eee",
                border_color="#aaa",
                border_width=1,
                border_radius=4,
                rich={
                    "a": {"color": "#999", "lineHeight": 22, "align": "center"},
                    "abg": {
                        "backgroundColor": "#e3e3e3",
                        "width": "100%",
                        "align": "right",
                        "height": 22,
                        "borderRadius": [4, 4, 0, 0],
                    },
                    "hr": {
                        "borderColor": "#aaa",
                        "width": "100%",
                        "borderWidth": 0.5,
                        "height": 0,
                    },
                    "b": {"fontSize": 16, "lineHeight": 33},
                    "per": {
                        "color": "#eee",
                        "backgroundColor": "#334455",
                        "padding": [2, 4],
                        "borderRadius": 2,
                    },
                },
            ),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Pie-富文本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/58702177-9dca5100-83d7-11e9-9204-37441a51d444.png)

> Pie-多饼图基本示例

```python
def pie_multiple_base() -> Pie:
    fn = """
    function(params) {
        if(params.name == '其他')
            return '\\n\\n\\n' + params.name + ' : ' + params.value + '%';
        return params.name + ' : ' + params.value + '%';
    }
    """

    def new_label_opts():
        return opts.LabelOpts(formatter=JsCode(fn), position="center")

    c = (
        Pie()
        .add(
            "",
            [list(z) for z in zip(["剧情", "其他"], [25, 75])],
            center=["20%", "30%"],
            radius=[60, 80],
            label_opts=new_label_opts(),
        )
        .add(
            "",
            [list(z) for z in zip(["奇幻", "其他"], [24, 76])],
            center=["55%", "30%"],
            radius=[60, 80],
            label_opts=new_label_opts(),
        )
        .add(
            "",
            [list(z) for z in zip(["爱情", "其他"], [14, 86])],
            center=["20%", "70%"],
            radius=[60, 80],
            label_opts=new_label_opts(),
        )
        .add(
            "",
            [list(z) for z in zip(["惊悚", "其他"], [11, 89])],
            center=["55%", "70%"],
            radius=[60, 80],
            label_opts=new_label_opts(),
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Pie-多饼图基本示例"),
            legend_opts=opts.LegendOpts(
                type_="scroll", pos_top="20%", pos_left="80%", orient="vertical"
            ),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/63604758-26cfdd80-c5ff-11e9-9b94-46eeba85ecd9.png)


## Polar：极坐标系

> *class pyecharts.charts.Polar*

```python
class Polar(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Polar.add_schema*

```python
 def add_schema(
    radiusaxis_opts: Union[opts.RadiusAxisOpts, dict] = opts.RadiusAxisOpts(),
    angleaxis_opts: Union[opts.AngleAxisOpts, dict] = opts.AngleAxisOpts(),
)
```

> *func pyecharts.charts.Polar.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据项
    data: Sequence,

    # 是否选中图例
    is_selected: bool = True,

    # 图表类型，支持
    # ChartType.SCATTER, ChartType.LINE, ChartType.BAR，ChartType.EFFECT_SCATTER
    type_: str = "line",

    # ECharts 提供的标记类型包括 'circle', 'rect', 'roundRect', 'triangle', 
    # 'diamond', 'pin', 'arrow', 'none'
    # 可以通过 'image://url' 设置为图片，其中 URL 为图片的链接，或者 dataURI。
    symbol: Optional[str] = None,

    # 标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，
    # 例如 [20, 10] 表示标记宽为 20，高为 10。
    symbol_size: Numeric = 4,

    # 数据堆叠，同个类目轴上系列配置相同的　stack　值可以堆叠放置。
    stack: Optional[str] = None,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 区域填充样式配置项，参考 `series_options.AreaStyleOpts`
    areastyle_opts: Union[opts.AreaStyleOpts, dict] = opts.AreaStyleOpts(),

    # 坐标轴刻度配置项，参考 `global_options.AxisTickOpts`
    axistick_opts: Union[AxisTickOpts, dict, None] = None,

    # 涟漪特效配置项，参考 `series_options.EffectOpts`
    effect_opts: Union[opts.EffectOpts, dict] = opts.EffectOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,
)
```

### RadiusAxisItem：极坐标系径向轴数据项

> *class pyecharts.options.RadiusAxisItem*

```python
class RadiusAxisItem(
    value: Optional[str] = None,
    textstyle_opts: Optional[TextStyleOpts] = None,
)
```

### RadiusAxisOpts：极坐标系径向轴配置项

> *class pyecharts.options.RadiusAxisOpts*

```python
class RadiusAxisOpts(
    # 径向轴所在的极坐标系的索引，默认使用第一个极坐标系。
    polar_index: Optional[int] = None,

    # 数据项，参考 `global_options.RadiusAxisItem`
    data: Optional[Sequence[Union[RadiusAxisItem, dict, str]]] = None,

    # 坐标轴两边留白策略，类目轴和非类目轴的设置和表现不一样。
    # 类目轴中 boundaryGap 可以配置为 true 和 false。默认为 true，这时候刻度只是作为分隔线，
    # 标签和数据点都会在两个刻度之间的带(band)中间。
    # 非类目轴，包括时间，数值，对数轴，boundaryGap是一个两个值的数组，分别表示数据最小值和最大值的延伸范围
    # 可以直接设置数值或者相对的百分比，在设置 min 和 max 后无效。 示例：boundaryGap: ['20%', '20%']
    boundary_gap: Union[bool, Sequence] = None,

    # 坐标轴类型。可选：
    # 'value': 数值轴，适用于连续数据。
    # 'category': 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
    # 'time': 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同
    # 例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。
    # 'log' 对数轴。适用于对数数据。
    type_: Optional[str] = None,

    # 坐标轴名称。
    name: Optional[str] = None,

    # 坐标轴名称显示位置。可选：
    # 'start', 'middle' 或者 'center','end
    name_location: Optional[str] = None,

    # 坐标轴刻度最小值。
    # 可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。
    # 不设置时会自动计算最小值保证坐标轴刻度的均匀分布。
    # 在类目轴中，也可以设置为类目的序数（如类目轴 data: ['类A', '类B', '类C'] 中，序数 2 表示 '类C'
    # 也可以设置为负数，如 -3）。
    min_: Union[str, Numeric, None] = None,

    # 坐标轴刻度最大值。
    # 可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。
    # 不设置时会自动计算最大值保证坐标轴刻度的均匀分布。
    # 在类目轴中，也可以设置为类目的序数（如类目轴 data: ['类A', '类B', '类C'] 中，序数 2 表示 '类C'
    # 也可以设置为负数，如 -3）。
    max_: Union[str, Numeric, None] = None,

    # 只在数值轴中（type: 'value'）有效。
    # 是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。
    # 在设置 min 和 max 之后该配置项无效。
    is_scale: bool = False,
    
    # 强制设置坐标轴分割间隔。
    interval: Optional[Numeric] = None,

    # 分割线配置项，参考 `series_options.SplitLineOpts`
    splitline_opts: Union[SplitLineOpts, dict, None] = None,

    # 坐标轴在 grid 区域中的分隔区域，默认不显示。参考 `series_options.SplitAreaOpts`
    splitarea_opts: Union[SplitAreaOpts, dict, None] = None,

    # 坐标轴线风格配置项，参考 `series_options.AxisLineOpts`
    axisline_opts: Union[AxisLineOpts, dict, None] = None,

    # 坐标轴线标签配置项，参考 `series_options.LabelOpts`
    axislabel_opts: Union[LabelOpts, dict, None] = None,

    # 半径轴组件的所有图形的 z 值。控制图形的前后顺序。z 值 小的图形会被 z 值大的图形覆盖
    z: Optional[int] = None,
)
```

### AngleAxisItem：极坐标系角度轴数据项

> *class pyecharts.options.AngleAxisItem*

```python
class AngleAxisItem(
    value: Optional[str] = None,
    textstyle_opts: Optional[TextStyleOpts] = None,
)
```

### AngleAxisOpts：极坐标系角度轴配置项

> *class pyecharts.options.AngleAxisOpts*

```python
class AngleAxisOpts(
    # 径向轴所在的极坐标系的索引，默认使用第一个极坐标系。
    polar_index: Optional[int] = None,
    data: Optional[Sequence[Union[AngleAxisItem, dict, str]]] = None,
    start_angle: Optional[Numeric] = None,
    is_clockwise: bool = False,

    # 坐标轴两边留白策略，类目轴和非类目轴的设置和表现不一样。
    # 类目轴中 boundaryGap 可以配置为 true 和 false。默认为 true，这时候刻度只是作为分隔线，
    # 标签和数据点都会在两个刻度之间的带(band)中间。
    # 非类目轴，包括时间，数值，对数轴，boundaryGap是一个两个值的数组，分别表示数据最小值和最大值的延伸范围
    # 可以直接设置数值或者相对的百分比，在设置 min 和 max 后无效。 示例：boundaryGap: ['20%', '20%']
    boundary_gap: Union[bool, Sequence] = None,

    # 坐标轴类型。可选：
    # 'value': 数值轴，适用于连续数据。
    # 'category': 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
    # 'time': 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同
    # 例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。
    # 'log' 对数轴。适用于对数数据。
    type_: Optional[str] = None,

    # 坐标轴刻度最小值。
    # 可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。
    # 不设置时会自动计算最小值保证坐标轴刻度的均匀分布。
    # 在类目轴中，也可以设置为类目的序数（如类目轴 data: ['类A', '类B', '类C'] 中，序数 2 表示 '类C'
    # 也可以设置为负数，如 -3）。
    min_: Union[str, Numeric, None] = None,

    # 坐标轴刻度最大值。
    # 可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。
    # 不设置时会自动计算最大值保证坐标轴刻度的均匀分布。
    # 在类目轴中，也可以设置为类目的序数（如类目轴 data: ['类A', '类B', '类C'] 中，序数 2 表示 '类C'
    # 也可以设置为负数，如 -3）。
    max_: Union[str, Numeric, None] = None,

    # 只在数值轴中（type: 'value'）有效。
    # 是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。
    # 在设置 min 和 max 之后该配置项无效。
    is_scale: bool = False,

    # 坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整。
    # 在类目轴中无效。
    split_number: Numeric = 5,

    # 强制设置坐标轴分割间隔。
    interval: Optional[Numeric] = None,

    # 分割线风格配置项，参考 `series_options.SplitLineOpts`
    splitline_opts: Union[SplitLineOpts, dict, None] = None,

    # 坐标轴线风格配置项，参考 `series_options.AxisLineOpts`
    axisline_opts: Union[AxisLineOpts, dict, None] = None,

    # 坐标轴标签风格配置项，参考 `series_options.LabelOpts`
    axislabel_opts: Union[LabelOpts, dict, None] = None,

    # 半径轴组件的所有图形的 z 值。控制图形的前后顺序。z 值 小的图形会被 z 值大的图形覆盖
    z: Optional[int] = None,
)
```

### Demo

> Polar-Scatter0

```python
import math
import random

from pyecharts.faker import Faker
from pyecharts import options as opts
from pyecharts.charts import Page, Polar


def polar_scatter0() -> Polar:
    data = [(i, random.randint(1, 100)) for i in range(101)]
    c = (
        Polar()
        .add("", data, type_="scatter", label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(title_opts=opts.TitleOpts(title="Polar-Scatter0"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933279-5dfcae00-5c5f-11e9-8ee8-21721e663c1a.png)

> Polar-Scatter1

```python
def polar_scatter1() -> Polar:
    c = (
        Polar()
        .add("", [(10, random.randint(1, 100)) for i in range(300)], type_="scatter")
        .add("", [(11, random.randint(1, 100)) for i in range(300)], type_="scatter")
        .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(title_opts=opts.TitleOpts(title="Polar-Scatter1"))
    )

    return c
```
![](https://user-images.githubusercontent.com/19553554/55933321-88e70200-5c5f-11e9-93a8-5ca5a5143176.png)

> Polar-EffectScatter

```python
def polar_effectscatter() -> Polar:
    data = [(i, random.randint(1, 100)) for i in range(10)]
    c = (
        Polar()
        .add(
            "",
            data,
            type_="effectScatter",
            effect_opts=opts.EffectOpts(scale=10, period=5),
            label_opts=opts.LabelOpts(is_show=False),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Polar-EffectScatter"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933356-9f8d5900-5c5f-11e9-83bb-0abc240279b0.png)

> Polar-RadiusAxis

```python
def polar_radiusaxis() -> Polar:
    c = (
        Polar()
        .add_schema(
            radiusaxis_opts=opts.RadiusAxisOpts(data=Faker.week, type_="category")
        )
        .add("A", [1, 2, 3, 4, 3, 5, 1], type_="bar", stack="stack0")
        .add("B", [2, 4, 6, 1, 2, 3, 1], type_="bar", stack="stack0")
        .add("C", [1, 2, 3, 4, 1, 2, 5], type_="bar", stack="stack0")
        .set_global_opts(title_opts=opts.TitleOpts(title="Polar-RadiusAxis"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933386-b633b000-5c5f-11e9-9abb-331ba6eae0c7.png)

> Polar-AngleAxis

```python
def polar_angleaxis() -> Polar:
    c = (
        Polar()
        .add_schema(
            angleaxis_opts=opts.AngleAxisOpts(data=Faker.week, type_="category")
        )
        .add("A", [1, 2, 3, 4, 3, 5, 1], type_="bar", stack="stack0")
        .add("B", [2, 4, 6, 1, 2, 3, 1], type_="bar", stack="stack0")
        .add("C", [1, 2, 3, 4, 1, 2, 5], type_="bar", stack="stack0")
        .set_global_opts(title_opts=opts.TitleOpts(title="Polar-AngleAxis"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933405-c186db80-5c5f-11e9-8cab-81f323669d83.png)

> Polar-Love

```python
def polar_flower() -> Polar:
    data = []
    for i in range(101):
        theta = i / 100 * 360
        r = 5 * (1 + math.sin(theta / 180 * math.pi))
        data.append([r, theta])
    hour = [i for i in range(1, 25)]
    c = (
        Polar()
        .add_schema(
            angleaxis_opts=opts.AngleAxisOpts(
                data=hour, type_="value", boundary_gap=False, start_angle=0
            )
        )
        .add("love", data, label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(title_opts=opts.TitleOpts(title="Polar-Love"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933447-e3805e00-5c5f-11e9-83ed-2c97f7f43dea.png)

> Polar-Flower

```python
def polar_flower() -> Polar:
    data = []
    for i in range(361):
        t = i / 180 * math.pi
        r = math.sin(2 * t) * math.cos(2 * t)
        data.append([r, i])
    c = (
        Polar()
        .add_schema(angleaxis_opts=opts.AngleAxisOpts(start_angle=0, min_=0))
        .add("flower", data, label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(title_opts=opts.TitleOpts(title="Polar-Flower"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933460-eed38980-5c5f-11e9-87c4-6dfa265febda.png)


## Radar：雷达图

> *class pyecharts.charts.Radar*

```python
class Radar(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Radar.add_schema*

```python
def add_schema(
    # 雷达指示器配置项列表，参考 `RadarIndicatorItem`
    schema: Sequence[Union[opts.RadarIndicatorItem, dict]],

    # 雷达图绘制类型，可选 'polygon' 和 'circle'
    shape: Optional[str] = None,

    # 文字样式配置项，参考 `series_options.TextStyleOpts`
    textstyle_opts: Union[opts.TextStyleOpts, dict] = opts.TextStyleOpts(),

    # 分割线配置项，参考 `series_options.SplitLineOpts`
    splitline_opt: Union[opts.SplitLineOpts, dict] = opts.SplitLineOpts(is_show=True),

    # 分隔区域配置项，参考 `series_options.SplitAreaOpts`
    splitarea_opt: Union[opts.SplitAreaOpts, dict] = opts.SplitAreaOpts(),

    # 坐标轴轴线配置项，参考 `global_options.AxisLineOpts`
    axisline_opt: Union[opts.AxisLineOpts, dict] = opts.AxisLineOpts(),

    # 极坐标系的径向轴。参考 `basic_charts.RadiusAxisOpts`
    radiusaxis_opts: types.RadiusAxis = None,
    
    # 极坐标系的角度轴。参考 `basic_charts.AngleAxisOpts`
    angleaxis_opts: types.AngleAxis = None,

    # 极坐标系配置，参考 `global_options.PolorOpts`
    polar_opts: types.Polar = None,
)
```

> *func pyecharts.charts.Radar.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据项
    data: Sequence,

    # 是否选中图例
    is_selected: bool = True,

    # ECharts 提供的标记类型包括 'circle', 'rect', 'roundRect', 'triangle', 
    # 'diamond', 'pin', 'arrow', 'none'
    # 可以通过 'image://url' 设置为图片，其中 URL 为图片的链接，或者 dataURI。
    symbol: Optional[str] = None,

    # 系列 label 颜色
    color: Optional[str] = None,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: opts.LabelOpts = opts.LabelOpts(),

    # 线样式配置项，参考 `series_options.LineStyleOpts`
    linestyle_opts: opts.LineStyleOpts = opts.LineStyleOpts(),

    # 区域填充样式配置项，参考 `series_options.AreaStyleOpts`
    areastyle_opts: opts.AreaStyleOpts = opts.AreaStyleOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,
)
```

### RadarIndicatorItem

> *class pyecharts.options.RadarIndicatorItem*

```python
class RadarIndicatorItem(
    # 指示器名称。
    name: Optional[str] = None,

    # 指示器的最大值，可选，建议设置
    min_: Optional[Numeric] = None,

    # 指示器的最小值，可选，默认为 0。
    max_: Optional[Numeric] = None,

    # 标签特定的颜色。
    color: Optional[str] = None,
)
```

### Demo

> Radar-基本示例

```python
from pyecharts import options as opts
from pyecharts.charts import Radar


v1 = [[4300, 10000, 28000, 35000, 50000, 19000]]
v2 = [[5000, 14000, 28000, 31000, 42000, 21000]]


def radar_base() -> Radar:
    c = (
        Radar()
        .add_schema(
            schema=[
                opts.RadarIndicatorItem(name="销售", max_=6500),
                opts.RadarIndicatorItem(name="管理", max_=16000),
                opts.RadarIndicatorItem(name="信息技术", max_=30000),
                opts.RadarIndicatorItem(name="客服", max_=38000),
                opts.RadarIndicatorItem(name="研发", max_=52000),
                opts.RadarIndicatorItem(name="市场", max_=25000),
            ]
        )
        .add("预算分配", v1)
        .add("实际开销", v2)
        .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(title_opts=opts.TitleOpts(title="Radar-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933590-6bfefe80-5c60-11e9-8b15-0858f1b95e28.png)

> Radar-单例模式

```python
def radar_selected_mode() -> Radar:
    c = (
        Radar()
        .add_schema(
            schema=[
                opts.RadarIndicatorItem(name="销售", max_=6500),
                opts.RadarIndicatorItem(name="管理", max_=16000),
                opts.RadarIndicatorItem(name="信息技术", max_=30000),
                opts.RadarIndicatorItem(name="客服", max_=38000),
                opts.RadarIndicatorItem(name="研发", max_=52000),
                opts.RadarIndicatorItem(name="市场", max_=25000),
            ]
        )
        .add("预算分配", v1)
        .add("实际开销", v2)
        .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(
            legend_opts=opts.LegendOpts(selected_mode="single"),
            title_opts=opts.TitleOpts(title="Radar-单例模式"),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933615-8507af80-5c60-11e9-9e27-8ea17f6a0c0f.png)

> Radar-空气质量

```python
def radar_air_quality() -> Radar:
    value_bj = [
        [55, 9, 56, 0.46, 18, 6, 1],
        [25, 11, 21, 0.65, 34, 9, 2],
        [56, 7, 63, 0.3, 14, 5, 3],
        [33, 7, 29, 0.33, 16, 6, 4],
        [42, 24, 44, 0.76, 40, 16, 5],
        [82, 58, 90, 1.77, 68, 33, 6],
        [74, 49, 77, 1.46, 48, 27, 7],
        [78, 55, 80, 1.29, 59, 29, 8],
        [267, 216, 280, 4.8, 108, 64, 9],
        [185, 127, 216, 2.52, 61, 27, 10],
        [39, 19, 38, 0.57, 31, 15, 11],
        [41, 11, 40, 0.43, 21, 7, 12],
    ]
    value_sh = [
        [91, 45, 125, 0.82, 34, 23, 1],
        [65, 27, 78, 0.86, 45, 29, 2],
        [83, 60, 84, 1.09, 73, 27, 3],
        [109, 81, 121, 1.28, 68, 51, 4],
        [106, 77, 114, 1.07, 55, 51, 5],
        [109, 81, 121, 1.28, 68, 51, 6],
        [106, 77, 114, 1.07, 55, 51, 7],
        [89, 65, 78, 0.86, 51, 26, 8],
        [53, 33, 47, 0.64, 50, 17, 9],
        [80, 55, 80, 1.01, 75, 24, 10],
        [117, 81, 124, 1.03, 45, 24, 11],
        [99, 71, 142, 1.1, 62, 42, 12],
    ]
    c_schema = [
        {"name": "AQI", "max": 300, "min": 5},
        {"name": "PM2.5", "max": 250, "min": 20},
        {"name": "PM10", "max": 300, "min": 5},
        {"name": "CO", "max": 5},
        {"name": "NO2", "max": 200},
        {"name": "SO2", "max": 100},
    ]
    c = (
        Radar()
        .add_schema(schema=c_schema, shape="circle")
        .add("北京", value_bj, color="#f9713c")
        .add("上海", value_sh, color="#b3e4a1")
        .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(title_opts=opts.TitleOpts(title="Radar-空气质量"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933630-8fc24480-5c60-11e9-9fd6-740b11fd33b5.png)


> Radar-轴线（Polar）

```python
def radar_angle_radius_axis_opts() -> Radar:
    data = [
        {
            "value": [4, -4, 2, 3, 0, 1],
            "name": "预算分配"
        },
    ]
    c_schema = [
        {"name": "销售", "max": 4, "min": -4},
        {"name": "管理", "max": 4, "min": -4},
        {"name": "技术", "max": 4, "min": -4},
        {"name": "客服", "max": 4, "min": -4},
        {"name": "研发", "max": 4, "min": -4},
        {"name": "市场", "max": 4, "min": -4},
    ]
    c = (
        Radar()
        .set_colors(["#4587E7"])
        .add_schema(
            schema=c_schema,
            shape="circle",
            center=["50%", "50%"],
            radius="80%",
            angleaxis_opts=opts.AngleAxisOpts(
                min_=0,
                max_=360,
                is_clockwise=False,
                interval=5,
                axistick_opts=opts.AxisTickOpts(is_show=False),
                axislabel_opts=opts.LabelOpts(is_show=False),
                axisline_opts=opts.AxisLineOpts(is_show=False),
                splitline_opts=opts.SplitLineOpts(is_show=False),
            ),
            radiusaxis_opts=opts.RadiusAxisOpts(
                min_=-4,
                max_=4,
                interval=2,
                splitarea_opts=opts.SplitAreaOpts(
                    is_show=True,
                    areastyle_opts=opts.AreaStyleOpts(opacity=1),
                )
            ),
            polar_opts=opts.PolarOpts(),
            splitarea_opt=opts.SplitAreaOpts(is_show=False),
            splitline_opt=opts.SplitLineOpts(is_show=False),
        )
        .add(
            series_name="预算",
            data=data,
            areastyle_opts=opts.AreaStyleOpts(opacity=0.1),
            linestyle_opts=opts.LineStyleOpts(width=1),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/17564655/72131077-34231400-33b6-11ea-9a5c-d1ca8e3e94c3.png)


## Sankey：桑基图

> *class pyecharts.charts.Sankey*

```python
class Sankey(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *class pyechart.options.SankeyLevelsOpts*

```python
class SankeyLevelsOpts(
    # 指定设置的是桑基图哪一层，取值从 0 开始。
    depth: Numeric = None,

    # 桑基图指定层节点的样式。参考 `global_opts.ItemStyleOpts`
    itemstyle_opts: Union[ItemStyleOpts, dict, None] = None,

    # 桑基图指定层出边的样式。
    # 其中 lineStyle.color 支持设置为'source'或者'target'特殊值，此时出边会自动取源节点或目标节点的颜色作为自己的颜色。
    # 参考 `global_opts.LineStyleOpts`
    linestyle_opts: Union[LineStyleOpts, dict, None] = None,
)
```

> *func pyecharts.charts.Sankey.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,
    nodes: Sequence,
    links: Sequence,

    # 是否选中图例
    is_selected: bool = True,
    
    # Sankey 组件离容器左侧的距离。
    pos_left: types.Union[str, types.Numeric] = "5%",

    # Sankey 组件离容器上侧的距离。
    pos_top: types.Union[str, types.Numeric] = "5%",

    # Sankey 组件离容器右侧的距离。
    pos_right: types.Union[str, types.Numeric] = "20%",
    
    # Sankey 组件离容器下侧的距离。
    pos_bottom: types.Union[str, types.Numeric] = "5%",

    # 桑基图中每个矩形节点的宽度。
    node_width: Numeric = 20,

    # 桑基图中每一列任意两个矩形节点之间的间隔。
    node_gap: Numeric = 8,
    
    # 桑基图中节点的对齐方式，默认是双端对齐，可以设置为左对齐或右对齐，对应的值分别是：
    # justify: 节点双端对齐。
    # left: 节点左对齐。
    # right: 节点右对齐。
    node_align: str = "justify",
    
    # 布局的迭代次数，用来不断优化图中节点的位置，以减少节点和边之间的相互遮盖。
    # 默认布局迭代次数：32。
    # 注: 布局迭代次数不要低于默认值。
    layout_iterations: types.Numeric = 32,

    # 桑基图中节点的布局方向，可以是水平的从左往右，也可以是垂直的从上往下。
    # 对应的参数值分别是 horizontal, vertical。
    orient: str = "horizontal",

    # 控制节点拖拽的交互，默认开启。开启后，用户可以将图中任意节点拖拽到任意位置。若想关闭此交互，只需将值设为 false 就行了。
    is_draggable: bool = True,
    
    # 鼠标 hover 到节点或边上，相邻接的节点和边高亮的交互，默认关闭，可手动开启。
    # false：hover 到节点或边时，只有被 hover 的节点或边高亮。
    # true：同 'allEdges'。
    # 'allEdges'：hover 到节点时，与节点邻接的所有边以及边对应的节点全部高亮。hover 到边时，边和相邻节点高亮。
    # 'outEdges'：hover 的节点、节点的出边、出边邻接的另一节点 会被高亮。hover 到边时，边和相邻节点高亮。
    # 'inEdges'：hover 的节点、节点的入边、入边邻接的另一节点 会被高亮。hover 到边时，边和相邻节点高亮。
    focus_node_adjacency: types.Union[bool, str] = False,
    
    # 桑基图每一层的设置。可以逐层设置
    levels: types.SankeyLevel = None,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 线条样式配置项，参考 `series_options.LineStyleOpts`
    linestyle_opt: Union[opts.LineStyleOpts, dict] = opts.LineStyleOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,
)
```

### Demo

> Sankey-基本示例

```python
import json
import os

from pyecharts import options as opts
from pyecharts.charts import Page, Sankey


def sankey_base() -> Sankey:
    nodes = [
        {"name": "category1"},
        {"name": "category2"},
        {"name": "category3"},
        {"name": "category4"},
        {"name": "category5"},
        {"name": "category6"},
    ]

    links = [
        {"source": "category1", "target": "category2", "value": 10},
        {"source": "category2", "target": "category3", "value": 15},
        {"source": "category3", "target": "category4", "value": 20},
        {"source": "category5", "target": "category6", "value": 25},
    ]
    c = (
        Sankey()
        .add(
            "sankey",
            nodes,
            links,
            linestyle_opt=opts.LineStyleOpts(opacity=0.2, curve=0.5, color="source"),
            label_opts=opts.LabelOpts(position="right"),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Sankey-基本示例"))
    )

    return c
```
![](https://user-images.githubusercontent.com/19553554/55933773-137c3100-5c61-11e9-9af5-4096121d6848.png)

> Sankey-官方示例

```python
def sankey_offical() -> Sankey:
    with open(os.path.join("fixtures", "energy.json"), "r", encoding="utf-8") as f:
        j = json.load(f)
    c = (
        Sankey()
        .add(
            "sankey",
            nodes=j["nodes"],
            links=j["links"],
            linestyle_opt=opts.LineStyleOpts(opacity=0.2, curve=0.5, color="source"),
            label_opts=opts.LabelOpts(position="right"),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Sankey-官方示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933787-1ecf5c80-5c61-11e9-8217-cf34864a6ee9.png)

> Sankey-垂直布局

```python
def sankey_vertical() -> Sankey:
    colors = [
        "#67001f",
        "#b2182b",
        "#d6604d",
        "#f4a582",
        "#fddbc7",
        "#d1e5f0",
        "#92c5de",
        "#4393c3",
        "#2166ac",
        "#053061",
    ]
    nodes = [
        {"name": "a"},
        {"name": "b"},
        {"name": "a1"},
        {"name": "b1"},
        {"name": "c"},
        {"name": "e"},
    ]
    links = [
        {"source": "a", "target": "a1", "value": 5},
        {"source": "e", "target": "b", "value": 3},
        {"source": "a", "target": "b1", "value": 3},
        {"source": "b1", "target": "a1", "value": 1},
        {"source": "b1", "target": "c", "value": 2},
        {"source": "b", "target": "c", "value": 1},
    ]
    c = (
        Sankey()
        .set_colors(colors)
        .add(
            "sankey",
            nodes=nodes,
            links=links,
            pos_bottom="10%",
            focus_node_adjacency="allEdges",
            orient="vertical",
            linestyle_opt=opts.LineStyleOpts(opacity=0.2, curve=0.5, color="source"),
            label_opts=opts.LabelOpts(position="top"),
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Sankey-Vertical"),
            tooltip_opts=opts.TooltipOpts(trigger="item", trigger_on="mousemove"),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/17564655/72131198-86fccb80-33b6-11ea-815e-b04f7297c7e4.png)

> Sankey-With Level Setting

```python
def sankey_with_level_setting() -> Sankey:
    with open(os.path.join("fixtures", "product.json"), "r", encoding="utf-8") as f:
        j = json.load(f)
    c = (
        Sankey()
        .add(
            "sankey",
            nodes=j["nodes"],
            links=j["links"],
            pos_top="10%",
            focus_node_adjacency=True,
            levels=[
                opts.SankeyLevelsOpts(
                    depth=0,
                    itemstyle_opts=opts.ItemStyleOpts(color="#fbb4ae"),
                    linestyle_opts=opts.LineStyleOpts(color="source", opacity=0.6),
                ),
                opts.SankeyLevelsOpts(
                    depth=1,
                    itemstyle_opts=opts.ItemStyleOpts(color="#b3cde3"),
                    linestyle_opts=opts.LineStyleOpts(color="source", opacity=0.6),
                ),
                opts.SankeyLevelsOpts(
                    depth=2,
                    itemstyle_opts=opts.ItemStyleOpts(color="#ccebc5"),
                    linestyle_opts=opts.LineStyleOpts(color="source", opacity=0.6),
                ),
                opts.SankeyLevelsOpts(
                    depth=3,
                    itemstyle_opts=opts.ItemStyleOpts(color="#decbe4"),
                    linestyle_opts=opts.LineStyleOpts(color="source", opacity=0.6),
                ),
            ],
            linestyle_opt=opts.LineStyleOpts(curve=0.5),
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Sankey-Level Settings"),
            tooltip_opts=opts.TooltipOpts(trigger="item", trigger_on="mousemove"),
        )
    )
    return c
```
![](https://user-images.githubusercontent.com/17564655/72131243-a09e1300-33b6-11ea-9e72-7da0d292dc8f.png)

## Sunburst：旭日图

> *class pyecharts.charts.Sunburst*

```python
class Sunburst(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.Sunburst.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,
    
    # 数据项。
    data_pair: Sequence,
    
    # 旭日图的中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标。
    # 支持设置成百分比，设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度。
    center: Optional[Sequence] = None,
    
    # 旭日图的半径。可以为如下类型：
    # Sequence.<int|str>：数组的第一项是内半径，第二项是外半径。
    radius: Optional[Sequence] = None,
    
    # 当鼠标移动到一个扇形块时，可以高亮相关的扇形块。
    # 'descendant'：高亮该扇形块和后代元素，其他元素将被淡化；
    # 'ancestor'：高亮该扇形块和祖先元素；
    # 'self'：只高亮自身；
    # 'none'：不会淡化其他元素。
    highlight_policy: str = "descendant",
    
    # 点击节点后的行为。可取值为：false：节点点击无反应。
    # 'rootToNode'：点击节点后以该节点为根结点。
    # 'link'：如果节点数据中有 link 点击节点后会进行超链接跳转。
    node_click: str = "rootToNode",
    
    # 扇形块根据数据 value 的排序方式，如果未指定 value，则其值为子元素 value 之和。
    # 'desc'：降序排序；
    # 'asc'：升序排序；
    # 'null'：表示不排序，使用原始数据的顺序；
    # 使用 javascript 回调函数进行排列：
    sort_: Optional[JSFunc] = "desc",
    
    # 旭日图多层级配置
    # 目前配置方式可以参考: https://www.echartsjs.com/option.html#series-sunburst.levels
    levels: Optional[Sequence] = None,
    
    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),
    
    # 数据项的配置，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

### SunburstItem: 旭日图的数据项

> *class pyecharts.options.SunburstItem*

```python
class SunburstItem(
    # 数据值，如果包含 children，则可以不写 value 值。
    # 这时，将使用子元素的 value 之和作为父元素的 value。
    # 如果 value 大于子元素之和，可以用来表示还有其他子元素未显示。
    value: Optional[Numeric] = None,
    
    # 显示在扇形块中的描述文字。
    name: Optional[str] = None,
    
    # 点击此节点可跳转的超链接。须 Sunburst.add.node_click 值为 'link' 时才生效
    link: Optional[str] = None,
    
    # 意义同 HTML <a> 标签中的 target，跳转方式的不同
    # blank 是在新窗口或者新的标签页中打开
    # self 则在当前页面或者当前标签页打开
    target: Optional[str] = "blank",
    
    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[LabelOpts, dict, None] = None,
    
    # 数据项配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[ItemStyleOpts, dict, None] = None,
    
    # 子节点数据项配置配置(和 SunburstItem 一致, 递归下去)
    children: Optional[Sequence] = None,
)
```

### Demo

> Sunburst-基本示例

```python
from pyecharts import options as opts
from pyecharts.charts import Sunburst


def sunburst_base() -> Sunburst:
    data = [
        opts.SunburstItem(
            name="Grandpa",
            children=[
                opts.SunburstItem(
                    name="Uncle Leo",
                    value=15,
                    children=[
                        opts.SunburstItem(name="Cousin Jack", value=2),
                        opts.SunburstItem(
                            name="Cousin Mary",
                            value=5,
                            children=[opts.SunburstItem(name="Jackson", value=2)],
                        ),
                        opts.SunburstItem(name="Cousin Ben", value=4),
                    ],
                ),
                opts.SunburstItem(
                    name="Father",
                    value=10,
                    children=[
                        opts.SunburstItem(name="Me", value=5),
                        opts.SunburstItem(name="Brother Peter", value=1),
                    ],
                ),
            ],
        ),
        opts.SunburstItem(
            name="Nancy",
            children=[
                opts.SunburstItem(
                    name="Uncle Nike",
                    children=[
                        opts.SunburstItem(name="Cousin Betty", value=1),
                        opts.SunburstItem(name="Cousin Jenny", value=2),
                    ],
                )
            ],
        ),
    ]

    c = (
        Sunburst()
        .add(series_name="", data_pair=data, radius=[0, "90%"])
        .set_global_opts(title_opts=opts.TitleOpts(title="Sunburst-基本示例"))
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}"))
    )
    return c
```
![](https://user-images.githubusercontent.com/17564655/57566356-1ef87e80-73fe-11e9-8ce0-b9f94e4b2231.png)

> Sunburst-官方示例

```python
def sunburst_official() -> Sunburst:
    with open(os.path.join("fixtures", "drink.json"), "r", encoding="utf-8") as f:
        j = json.load(f)

    c = (
        Sunburst(init_opts=opts.InitOpts(width="1000px", height="600px"))
        .add(
            "",
            data_pair=j,
            highlight_policy="ancestor",
            radius=[0, "95%"],
            sort_="null",
            levels=[
                {},
                {
                    "r0": "15%",
                    "r": "35%",
                    "itemStyle": {"borderWidth": 2},
                    "label": {"rotate": "tangential"},
                },
                {"r0": "35%", "r": "70%", "label": {"align": "right"}},
                {
                    "r0": "70%",
                    "r": "72%",
                    "label": {"position": "outside", "padding": 3, "silent": False},
                    "itemStyle": {"borderWidth": 3},
                },
            ],
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="Sunburst-官方示例"))
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}"))
    )
    return c
```
![](https://user-images.githubusercontent.com/17564655/57567164-bdd5a880-7407-11e9-8d19-9be2776c57fa.png)


## ThemeRiver：主题河流图

> *class pyecharts.charts.ThemeRiver*

```python
class ThemeRiver(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.ThemeRiver.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: Sequence,

    # 系列数据项
    data: Sequence,

    # 是否选中图例
    is_selected: bool = True,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 单轴组件配置项，参考 `global_options.SingleAxisOpts`
    singleaxis_opts: Union[opts.SingleAxisOpts, dict] = opts.SingleAxisOpts(),
):
```

### Demo

> ThemeRiver-基本示例

```python
from pyecharts import options as opts
from pyecharts.charts import Page, ThemeRiver


def themeriver_example() -> ThemeRiver:
    data = [
        ["2015/11/08", 10, "DQ"],
        ["2015/11/09", 15, "DQ"],
        ["2015/11/10", 35, "DQ"],
        ["2015/11/14", 7, "DQ"],
        ["2015/11/15", 2, "DQ"],
        ["2015/11/16", 17, "DQ"],
        ["2015/11/17", 33, "DQ"],
        ["2015/11/18", 40, "DQ"],
        ["2015/11/19", 32, "DQ"],
        ["2015/11/20", 26, "DQ"],
        ["2015/11/08", 35, "TY"],
        ["2015/11/09", 36, "TY"],
        ["2015/11/10", 37, "TY"],
        ["2015/11/11", 22, "TY"],
        ["2015/11/12", 24, "TY"],
        ["2015/11/13", 26, "TY"],
        ["2015/11/14", 34, "TY"],
        ["2015/11/15", 21, "TY"],
        ["2015/11/16", 18, "TY"],
        ["2015/11/17", 45, "TY"],
        ["2015/11/18", 32, "TY"],
        ["2015/11/19", 35, "TY"],
        ["2015/11/20", 30, "TY"],
        ["2015/11/08", 21, "SS"],
        ["2015/11/09", 25, "SS"],
        ["2015/11/10", 27, "SS"],
        ["2015/11/11", 23, "SS"],
        ["2015/11/12", 24, "SS"],
        ["2015/11/13", 21, "SS"],
        ["2015/11/14", 35, "SS"],
        ["2015/11/15", 39, "SS"],
        ["2015/11/16", 40, "SS"],
        ["2015/11/17", 36, "SS"],
        ["2015/11/18", 33, "SS"],
        ["2015/11/19", 43, "SS"],
        ["2015/11/20", 40, "SS"],
        ["2015/11/14", 7, "QG"],
        ["2015/11/15", 2, "QG"],
        ["2015/11/16", 17, "QG"],
        ["2015/11/17", 33, "QG"],
        ["2015/11/18", 40, "QG"],
        ["2015/11/19", 32, "QG"],
        ["2015/11/20", 26, "QG"],
        ["2015/11/21", 35, "QG"],
        ["2015/11/22", 40, "QG"],
        ["2015/11/23", 32, "QG"],
        ["2015/11/24", 26, "QG"],
        ["2015/11/25", 22, "QG"],
        ["2015/11/08", 10, "SY"],
        ["2015/11/09", 15, "SY"],
        ["2015/11/10", 35, "SY"],
        ["2015/11/11", 38, "SY"],
        ["2015/11/12", 22, "SY"],
        ["2015/11/13", 16, "SY"],
        ["2015/11/14", 7, "SY"],
        ["2015/11/15", 2, "SY"],
        ["2015/11/16", 17, "SY"],
        ["2015/11/17", 33, "SY"],
        ["2015/11/18", 40, "SY"],
        ["2015/11/19", 32, "SY"],
        ["2015/11/20", 26, "SY"],
        ["2015/11/21", 35, "SY"],
        ["2015/11/22", 4, "SY"],
        ["2015/11/23", 32, "SY"],
        ["2015/11/24", 26, "SY"],
        ["2015/11/25", 22, "SY"],
        ["2015/11/08", 10, "DD"],
        ["2015/11/09", 15, "DD"],
        ["2015/11/10", 35, "DD"],
        ["2015/11/11", 38, "DD"],
        ["2015/11/12", 22, "DD"],
        ["2015/11/13", 16, "DD"],
        ["2015/11/14", 7, "DD"],
        ["2015/11/15", 2, "DD"],
        ["2015/11/16", 17, "DD"],
        ["2015/11/17", 33, "DD"],
        ["2015/11/18", 4, "DD"],
        ["2015/11/19", 32, "DD"],
        ["2015/11/20", 26, "DD"],
    ]
    c = (
        ThemeRiver()
        .add(
            ["DQ", "TY", "SS", "QG", "SY", "DD"],
            data,
            singleaxis_opts=opts.SingleAxisOpts(type_="time", pos_bottom="10%"),
        )
        .set_global_opts(title_opts=opts.TitleOpts(title="ThemeRiver-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55933910-7b327c00-5c61-11e9-9812-95073eaaa9bd.png)


## WordCloud：词云图

> *class pyecharts.charts.WordCloud*

```python
class WordCloud(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

> *func pyecharts.charts.WordCloud.add*

```python
def add(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据项，[(word1, count1), (word2, count2)]
    data_pair: Sequence,

    # 词云图轮廓，有 'circle', 'cardioid', 'diamond', 'triangle-forward', 'triangle', 'pentagon', 'star' 可选
    shape: str = "circle",

    # 单词间隔
    word_gap: Numeric = 20,

    # 单词字体大小范围
    word_size_range=None,

    # 旋转单词角度
    rotate_step: Numeric = 45,

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,
)
```

### Demo

> WordCloud-基本示例

```python
from pyecharts import options as opts
from pyecharts.charts import Page, WordCloud
from pyecharts.globals import SymbolType


words = [
    ("Sam S Club", 10000),
    ("Macys", 6181),
    ("Amy Schumer", 4386),
    ("Jurassic World", 4055),
    ("Charter Communications", 2467),
    ("Chick Fil A", 2244),
    ("Planet Fitness", 1868),
    ("Pitch Perfect", 1484),
    ("Express", 1112),
    ("Home", 865),
    ("Johnny Depp", 847),
    ("Lena Dunham", 582),
    ("Lewis Hamilton", 555),
    ("KXAN", 550),
    ("Mary Ellen Mark", 462),
    ("Farrah Abraham", 366),
    ("Rita Ora", 360),
    ("Serena Williams", 282),
    ("NCAA baseball tournament", 273),
    ("Point Break", 265),
]


def wordcloud_base() -> WordCloud:
    c = (
        WordCloud()
        .add("", words, word_size_range=[20, 100])
        .set_global_opts(title_opts=opts.TitleOpts(title="WordCloud-基本示例"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55934373-ecbefa00-5c62-11e9-950f-0d93aeb10a74.png)

> WordCloud-shape-diamond

```python
def wordcloud_diamond() -> WordCloud:
    c = (
        WordCloud()
        .add("", words, word_size_range=[20, 100], shape=SymbolType.DIAMOND)
        .set_global_opts(title_opts=opts.TitleOpts(title="WordCloud-shape-diamond"))
    )
    return c
```
![](https://user-images.githubusercontent.com/19553554/55934388-fb0d1600-5c62-11e9-8906-958aadc5c1a2.png)
