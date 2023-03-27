---
share: true
---


## Open
```dataview
TABLE
task,
when,
prior,
tdaz
FROM ""
FLATTEN action AS A
FLATTEN split(A,"\| ")[0] AS status
FLATTEN split(A,"\| ")[1] AS task
FLATTEN split(A,"\| ")[2] AS when
FLATTEN split(A,"\| ")[3] AS prior
FLATTEN split(A,"\| ")[4] AS tdaz
WHERE contains(status, "Open")
SORT tdaz DESC,prior, when
```

## Wait
```dataview
TABLE
task,
when,
prior
FROM ""
FLATTEN action AS A
FLATTEN split(A,"\| ")[0] AS status
FLATTEN split(A,"\| ")[1] AS task
FLATTEN split(A,"\| ")[2] AS when
FLATTEN split(A,"\| ")[3] AS prior
WHERE contains(status, "Wait")
SORT prior, when
```
## Next
```dataview
TABLE
task,
when,
prior
FROM ""
FLATTEN action AS A
FLATTEN split(A,"\| ")[0] AS status
FLATTEN split(A,"\| ")[1] AS task
FLATTEN split(A,"\| ")[2] AS when
FLATTEN split(A,"\| ")[3] AS prior
WHERE contains(status, "Next")
SORT prior, when
```

## Closed
```dataview
TABLE
status,
task,
when,
prior
FROM ""
FLATTEN action AS A
FLATTEN split(A,"\| ")[0] AS status
FLATTEN split(A,"\| ")[1] AS task
FLATTEN split(A,"\| ")[2] AS when
FLATTEN split(A,"\| ")[3] AS prior
WHERE contains(status, "Closed")
SORT prior, when
```
## Calendar

```dataview
CALENDAR
date
FROM ""
WHERE action
FLATTEN action AS A
FLATTEN split(A,"\| ")[0] AS status
FLATTEN split(A,"\| ")[1] AS task
FLATTEN split(A,"\| ")[2] AS when
FLATTEN date(split(when, " ")[0] + "T00:00:00") AS date
FLATTEN split(A,"\| ")[3] AS prior
where contains(status,"Open")
```

## Todo

```dataview
TABLE
task
FROM ""
WHERE todo
FLATTEN todo AS A
FLATTEN split(A,"\| ")[0] AS task
```

## Links to this Page
```dataviewjs
dv.list(
dv.pages(`[[${this.currentFilePath}]]`)
.map(page=>page.file.link)
)
```
```dataviewjs
dv.list(
dv.pages(`[[${this.currentFilePath}]]`)
.map(page=>page.file.inlinks)
)
```

## Notes
https://forum.obsidian.md/t/using-advanced-tables-with-dataview-for-work-hours-and-financial-calculation/37797/10
https://forum.obsidian.md/t/creating-a-tag-index-table-with-dataview/23997/12
https://blacksmithgu.github.io/obsidian-dataview/queries/structure/

Check [[Open Stack]] 
action:: Closed | start this now | 2023-01-10 | 2

