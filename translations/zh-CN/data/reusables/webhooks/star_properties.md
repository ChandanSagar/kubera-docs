| 键            | 类型    | 描述                                                                                        |
| ------------ | ----- | ----------------------------------------------------------------------------------------- |
| `action`     | `字符串` | 执行的操作。 可以是 `created` 或 `deleted`。                                                         |
| `starred_at` | `字符串` | 星标创建的时间。 {% data reusables.shortdesc.iso_8601 %} Will be `null` for the `deleted` action. |