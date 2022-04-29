# Analytics API

Một số pipelines trong aggregate cần chú ý

Trong <mark style="color:red;">**getAnalyticsByPageId**</mark>** function là hàm chạy aggregate để lấy các metric cho một page riêng biệt**

* Lấy các docs theo shopDomain, pageId và time theo query

```
{
  $match: {
    $and: [
      {shopDomain},
      {pageId},
      {time: {$gte: startTime, $lte: endTime}}
    ]
  }
}     
```

* Groups theo pageId và add session, visitor vào set để count
  * cRates: là conversion rate metric, tính tổng số lượng docs mà trong đó elêm
  * view(page views metrics): tính tổng số lượng click lên các elementType có linkToProduct như ProductMedia, ProductImage, ProductViewDetail

```
{
  $group: {
    _id: { pageId: "$pageId" },
    sessions: { $addToSet: "$sessionId" },
    visitors: { $addToSet: "$userId" },
    cRates: {
      $sum: {
        $cond: [{$in: ["$elementType", ["ProductATC", "ProductMedia", "ProductViewDetails", "ProductImage"]]}, 1, 0]
      }
    },
    views: {
      $sum: {
        $cond: [{$in: ["$elementType", ["ProductMedia", "ProductViewDetails", "ProductImage"]]}, 1, 0]
      }
    },
    atcs: {
      $sum: {
        $cond: [{$eq: ["$elementType", "ProductATC"]}, 1, 0]
      }
    },
    revenue: { $sum: "$revenue" }
  }
}
```

* Dùng denominator để tránh error divideByZero và sau đấy chia các fields được tính ở trên cho tổng sessions để lấy giá trị các metrics cần trả về.

```
 {
        $addFields: {
          denominator: {$cond: [{$gte: [{$size: "$sessions"}, 1]}, {$size: "$sessions"}, 1]}
        }
      },
      {
        $addFields: {
          sessions: {$size: "$sessions"},
          visitors: {$size: "$visitors"},
          cRates: {
            $divide: ["$cRates", "$denominator"]
          },
          atcs: {
            $divide: ["$atcs", "$denominator"]
          },
          views: {
            $divide: ["$views", "$denominator"]
          }
        }
      },
```
