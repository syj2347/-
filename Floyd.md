---
tags: [Code]
title: Floyd
created: '2022-09-02T13:11:28.445Z'
modified: '2022-09-02T13:11:41.512Z'
---

# Floyd
```cpp
void floyd()
{
    int i,j,k;
    for(k=1;k<=n;k++)
        for(i=1;i<=n;i++)
            for(j=1;j<=n;j++)
                    Map[i][j]=min(Map[i][j],Map[i][k]+Map[k][j]);
}
```
