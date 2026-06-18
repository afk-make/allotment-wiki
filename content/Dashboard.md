---
dashboard_month: Jul
---

## 🌴 Currently Growing
---
```dataview
TABLE
category,
location,
cultivation_type
FROM "Plants"
WHERE currently_growing = true
SORT category ASC
```




## 📋 Planned Crops
```dataview
TABLE
category,
plant_out_from,
plant_out_to
FROM "Plants"
WHERE planned = true
SORT plant_out_from ASC
```

```dataview
TABLE WITHOUT ID
category AS "Category",
length(rows) AS "Count"
FROM "Plants"
WHERE planned = true
GROUP BY category
SORT category
```


---



## 📅 KanBan

[[To Do Kanban]]
```dataview
TABLE
category,
added_to_kanban
FROM "Plants"
WHERE planned = true
SORT added_to_kanban ASC
```

## 🏠 Sow Indoors This Month

```dataviewjs  
const monthOrder = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];  
  
const selectedMonth = String(dv.current().dashboard_month).trim();  
  
dv.paragraph(`Showing: **${selectedMonth}**`);  
  
function inRange(month, from, to) {  
if (!from || !to) return false;  
  
const m = monthOrder.indexOf(String(month).trim());  
const f = monthOrder.indexOf(String(from).trim());  
const t = monthOrder.indexOf(String(to).trim());  
  
if (m < 0 || f < 0 || t < 0) return false;  
  
return f <= t  
? m >= f && m <= t  
: m >= f || m <= t;  
}  
  
dv.table(  
["Plant", "Sow Indoors", "Planned"],  
dv.pages('"Plants"')  
.where(p => p.planned === true)  
.where(p => inRange(selectedMonth, p.sow_indoors_from, p.sow_indoors_to))  
.sort(p => p.file.name)  
.map(p => [  
p.file.link,  
`${p.sow_indoors_from ?? ""}–${p.sow_indoors_to ?? ""}`,  
p.planned  
])  
);  
```


## 🌱 Sow Outdoors This Month
```dataviewjs
const monthOrder = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];

const selectedMonth = String(dv.current().dashboard_month).trim();

dv.paragraph(`Showing: **${selectedMonth}**`);

function inRange(month, from, to) {
  if (!from || !to) return false;

  const m = monthOrder.indexOf(String(month).trim());
  const f = monthOrder.indexOf(String(from).trim());
  const t = monthOrder.indexOf(String(to).trim());

  if (m < 0 || f < 0 || t < 0) return false;

  return f <= t
    ? m >= f && m <= t
    : m >= f || m <= t;
}

dv.table(
  ["Plant", "Sow Outdoors", "Planned"],
  dv.pages('"Plants"')
    .where(p => p.planned === true)
    .where(p => inRange(selectedMonth, p.sow_outdoors_from, p.sow_outdoors_to))
    .sort(p => p.file.name)
    .map(p => [
      p.file.link,
      `${p.sow_outdoors_from ?? ""}–${p.sow_outdoors_to ?? ""}`,
      p.planned
    ])
);
```


## 🥔 Plant Out This Month

```dataviewjs
const monthOrder = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];

const selectedMonth = String(dv.current().dashboard_month).trim();

dv.paragraph(`Showing: **${selectedMonth}**`);

function inRange(month, from, to) {
  if (!from || !to) return false;

  const m = monthOrder.indexOf(String(month).trim());
  const f = monthOrder.indexOf(String(from).trim());
  const t = monthOrder.indexOf(String(to).trim());

  if (m < 0 || f < 0 || t < 0) return false;

  return f <= t
    ? m >= f && m <= t
    : m >= f || m <= t;
}

dv.table(
  ["Plant", "Plant Out", "Planned"],
  dv.pages('"Plants"')
    .where(p => p.planned === true)
    .where(p => inRange(selectedMonth, p.plant_out_from, p.plant_out_to))
    .sort(p => p.file.name)
    .map(p => [
      p.file.link,
      `${p.plant_out_from ?? ""}–${p.plant_out_to ?? ""}`,
      p.planned
    ])
);
```



## 🍽 Harvest This Month

```dataviewjs
const monthOrder = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];

const selectedMonth = String(dv.current().dashboard_month).trim();

dv.paragraph(`Showing: **${selectedMonth}**`);

function inRange(month, from, to) {
  if (!from || !to) return false;

  const m = monthOrder.indexOf(String(month).trim());
  const f = monthOrder.indexOf(String(from).trim());
  const t = monthOrder.indexOf(String(to).trim());

  if (m < 0 || f < 0 || t < 0) return false;

  return f <= t
    ? m >= f && m <= t
    : m >= f || m <= t;
}

dv.table(
  ["Plant", "Harvest", "Flavour", "Growing"],
  dv.pages('"Plants"')
    .where(p => p.currently_growing === true)
    .where(p => inRange(selectedMonth, p.harvest_from, p.harvest_to))
    .sort(p => p.file.name)
    .map(p => [
      p.file.link,
      `${p.harvest_from ?? ""}–${p.harvest_to ?? ""}`,
      p.flavour,
      p.currently_growing
    ])
);
```



## 😫 Do Not Grow Again

```dataview
TABLE
personal_rating
FROM "Plants"
WHERE grow_again = false
```




## 🌳 Perennials

```dataview
TABLE
category,
cultivation_type,
location
FROM "Plants"
WHERE perennial = true
SORT name ASC
```



## ⭐ Top Rated

```dataview
TABLE
personal_rating,
flavour_rating
FROM ""
WHERE personal_rating
SORT personal_rating DESC
LIMIT 10
```



