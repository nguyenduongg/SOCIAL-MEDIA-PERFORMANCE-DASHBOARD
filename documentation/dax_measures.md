# DAX Measures

## Total Posts

- **Table ID:** `4727`
- **Format:** `0`

```DAX
COUNTROWS(Fact_PostPerformance)
```

## Total Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Views])
```

## Total Impressions

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Impressions])
```

## Total Clicks

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Clicks])
```

## Total Video Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Video_Views])
```

## Total Live Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Live_Stream_Views])
```

## Total Likes

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Likes])
```

## Total Comments

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Comments])
```

## Total Shares

- **Table ID:** `4727`
- **Format:** `0`

```DAX
SUM(Fact_PostPerformance[Shares])
```

## Average Views/Post

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Views],
    [Total Posts]
)
```

## Average Likes/Post

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Likes],
    [Total Posts]
)
```

## Average Comments/Post

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Comments],
    [Total Posts]
)
```

## Average Shares/Post

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Shares],
    [Total Posts]
)
```

## CTR

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Clicks],
    [Total Impressions]
)
```

## Engagement Rate

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Likes] + [Total Comments] + [Total Shares],
    [Total Views]
)
```

## Like Rate

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Likes],
    [Total Views]
)
```

## Comment Rate

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Comments],
    [Total Views]
)
```

## Share Rate

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Shares],
    [Total Views]
)
```

## Platform Rank by Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
RANKX(
    ALL(Dim_Platform[Platform]),
    [Total Views],
    ,
    DESC,
    DENSE
)
```

## Region Rank by Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
RANKX(
    ALL(Dim_Region[Region]),
    [Total Views],
    ,
    DESC,
    DENSE
)
```

## Platform View Share %

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Views],
    CALCULATE(
        [Total Views],
        ALL(Dim_Platform)
    )
)
```

## Region View Share %

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Views],
    CALCULATE(
        [Total Views],
        ALL(Dim_Region)
    )
)
```

## Previous Month Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
CALCULATE(
    [Total Views],
    DATEADD(Dim_Date[Post_Date], -1, MONTH)
)
```

## MoM Growth %

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
DIVIDE(
    [Total Views] - [Previous Month Views],
    [Previous Month Views]
)
```

## Running Total Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
CALCULATE(
    [Total Views],
    FILTER(
        ALL(Dim_Date[Post_Date]),
        Dim_Date[Post_Date] <= MAX(Dim_Date[Post_Date])
    )
)
```

## Total Engagement

- **Table ID:** `4727`
- **Format:** `0.0`

```DAX
[Total Likes]
+
[Total Comments]
+
[Total Shares]
```

## Top Platform

- **Table ID:** `4727`

```DAX
VAR TopPlatform =
    TOPN(
        1,
        VALUES(Dim_Platform[Platform]),
        [Average Views per Post],
        DESC
    )
RETURN
    MAXX(TopPlatform, Dim_Platform[Platform])
```

## Top Platform Views

- **Table ID:** `4727`
- **Format:** `0`

```DAX
VAR TopPlatform =
    TOPN(
        1,
        VALUES(Dim_Platform[Platform]),
        [Total Views],
        DESC
    )
RETURN
CALCULATE(
    [Total Views],
    TopPlatform
)
```

## Executive Insight

- **Table ID:** `4727`

```DAX
"Top Platform: "
&
[Top Platform]
&
UNICHAR(10)
&
"Views: "
&
FORMAT([Top Platform Views],"#,##0")
```

## Executive Insight 2

- **Table ID:** `4727`

```DAX
VAR Share =
DIVIDE(
    [Top Platform Views],
    [Total Views]
)
RETURN
"Contributes "
&
FORMAT(Share,"0.0%")
&
" of total views"
&
UNICHAR(10)
&
"Focus future campaigns"
```

## Color_MoM

- **Table ID:** `4727`

```DAX
VAR _val = [MoM Growth %]
RETURN IF(_val >= 0, "#00875A", "#DE350B")
```

## Average Views per Post

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Views],
    [Total Posts]
)
```

## Average Engagement per Post

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Engagement],
    [Total Posts]
)
```

## Overall Avg Views per Post

- **Table ID:** `4727`

```DAX
CALCULATE(
    [Average Views per Post],
    ALL(Dim_Platform)
)
```

## Platform Efficiency

- **Table ID:** `4727`

```DAX
VAR MaxViews =
    CALCULATE(
        MAXX(
            VALUES(Dim_Platform[Platform]),
            [Average Views per Post]
        ),
        ALL(Dim_Platform)
    )

VAR MaxEngagement =
    CALCULATE(
        MAXX(
            VALUES(Dim_Platform[Platform]),
            [Average Engagement per Post]
        ),
        ALL(Dim_Platform)
    )

VAR ViewsScore =
    DIVIDE(
        [Average Views per Post],
        MaxViews
    )

VAR EngagementScore =
    DIVIDE(
        [Average Engagement per Post],
        MaxEngagement
    )

RETURN
    0.6 * ViewsScore
    +
    0.4 * EngagementScore
```

## Most Efficient Platform

- **Table ID:** `4727`

```DAX
VAR T =
    TOPN(
        1,
        VALUES(Dim_Platform[Platform]),
        [Platform Efficiency],
        DESC
    )
RETURN
    MAXX(
        T,
        Dim_Platform[Platform]
    )
```

## Highest Platform Efficiency

- **Table ID:** `4727`

```DAX
MAXX(
    VALUES(Dim_Platform[Platform]),
    [Platform Efficiency]
)
```

## Average Views per Content

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Views],
    [Total Posts]
)
```

## Average Engagement per Content

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Engagement],
    [Total Posts]
)
```

## Content Share

- **Table ID:** `4727`

```DAX
DIVIDE(
    [Total Views],
    CALCULATE(
        [Total Views],
        ALL(Dim_Content)
    )
)
```

## Content Efficiency

- **Table ID:** `4727`

```DAX
0.6 *
DIVIDE(
    [Average Views per Content],
    CALCULATE(
        MAXX(
            VALUES(Dim_Content[Content_Category]),
            [Average Views per Content]
        ),
        ALL(Dim_Content)
    )
)
+
0.4 *
DIVIDE(
    [Average Engagement per Content],
    CALCULATE(
        MAXX(
            VALUES(Dim_Content[Content_Category]),
            [Average Engagement per Content]
        ),
        ALL(Dim_Content)
    )
)
```

## Most Efficient Content

- **Table ID:** `4727`

```DAX
VAR T =
    TOPN(
        1,
        VALUES(Dim_Content[Content_Category]),
        [Content Efficiency],
        DESC
    )
RETURN
    MAXX(
        T,
        Dim_Content[Content_Category]
    )
```

## Top Content Share

- **Table ID:** `4727`
- **Format:** `0.00%;-0.00%;0.00%`

```DAX
VAR TopContent =
    TOPN(
        1,
        VALUES(Dim_Content[Content_Category]),
        [Total Views],
        DESC
    )
RETURN
DIVIDE(
    MAXX(TopContent,[Total Views]),
    [Total Views]
)
```
