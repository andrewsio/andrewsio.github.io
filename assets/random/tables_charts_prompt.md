# Grocery tables and charts processing

I am going to share a structured csv with grocery data. Please produce structured tables and Chart.js code for visualizations. Do not produce commentary, narrative, or interpretation.

**TIME STRUCTURE**
Group all items by week number. Saturday is the start of the week.
Weeks must be labelled exactly as: “Week NN (YYYY)”.
If a calendar month spans four or five weeks, include all weeks that contain at least one day in that month.

**FIXED CATEGORIES**
Use exactly the categories shown in the category column.

**SHOPS VS BRANDS**
- Shop refers to the retailer (e.g., Ocado, Lidl, M&S store).
- Brand refers to the product manufacturer (e.g., M&S brand, Ocado brand, Other brand).
- These must be treated as separate dimensions and never inferred from one another.

**ORGANIC RULES**
- An item is organic only if relevant column is marked as yes. 

**UNIT DEFINITION**
- One unit is one unit, don't derive information from the item description. 

---

### OUTPUT PART 1: TABLES
Produce the following five tables with exact column names:

1. TABLE 1: WEEKLY SPEND BY CATEGORY (POUNDS)
Columns: Category, Week NN (YYYY) [for each week], Monthly total (£)

2. TABLE 2: WEEKLY FOOD SPEND BY SHOP (POUNDS)
Columns: Shop, Week NN (YYYY) [for each week], Monthly total (£)

3. TABLE 3: BRAND MIX BY SPEND (MONTHLY)
Rows: M&S, Ocado, Other. Columns: Brand, Monthly spend (£), Percentage of monthly food spend (%)

4. TABLE 4: ORGANIC VS NON-ORGANIC BY CATEGORY (MONTHLY, BY ITEM)
Columns: Category, Organic units, Non-organic units, Total units, Organic percentage (%)

5. TABLE 5: ORGANIC SHARE OVER TIME (WEEKLY)
Columns: Week NN (YYYY), Organic percentage by item (%), Organic percentage by spend (%)

---

### OUTPUT PART 2: VISUALIZATIONS
Populate the data in the following code blocks exactly as defined.

**1. Category Spend Stacked (Bar)**
```javascript
new Chart(document.getElementById('categorySpendStacked'), {
  type: 'bar',
  data: {
    labels: [/// per categories ///],
    datasets: [
      { label: 'Week 01', data: [/* data */] },
      { label: 'Week 02', data: [/* data */] },
      { label: 'Week 03', data: [/* data */] },
      { label: 'Week 04', data: [/* data */] }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Monthly spend by category (stacked by week)' } },
    scales: { x: { stacked: true }, y: { stacked: true, title: { display: true, text: 'Spend (£)' } } }
  }
});

```

**2. Shop Spend by Week (Bar)**

```javascript
new Chart(document.getElementById('shopSpendByWeek'), {
  type: 'bar',
  data: {
    labels: ['Week 01','Week 02','Week 03','Week 04'],
    datasets: [
      { label: 'Ocado', data: [/* data */], backgroundColor: '#6F2C91' },
      { label: 'Lidl', data: [/* data */], backgroundColor: '#0050AA' },
      { label: 'M&S (store)', data: [/* data */], backgroundColor: '#1F6A4D' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Food spend by shop, by week' } },
    scales: { x: { stacked: true }, y: { stacked: true, title: { display: true, text: 'Spend (£)' } } }
  }
});

```

**3. Brand Mix (Bar)**

```javascript
new Chart(document.getElementById('brandMix'), {
  type: 'bar',
  data: {
    labels: ['M&S','Ocado','Other'],
    datasets: [{
      label: '% of spend',
      data: [/* data */],
      backgroundColor: ['#1F6A4D','#6F2C91','#F28C28']
    }]
  },
  options: {
    plugins: { title: { display: true, text: 'Brand mix by spend' } },
    scales: { y: { max: 100, title: { display: true, text: '%' } } }
  }
});

```

**4. Organic Share by Category (Stacked Bar)**

```javascript
new Chart(document.getElementById('organicByCategory'), {
  type: 'bar',
  data: {
    labels: [/// per categories ///],
    datasets: [
      { label: 'Organic', data: [/* data */], backgroundColor: 'rgba(46, 125, 50, 0.75)' },
      { label: 'Non-organic', data: [/* data */], backgroundColor: 'rgba(200, 200, 200, 0.7)' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Organic share by category (monthly, by item)' } },
    scales: { x: { stacked: true }, y: { stacked: true, max: 100, title: { display: true, text: '% of items' } } }
  }
});

```

**5. Organic Share over Time (Line)**

```javascript
new Chart(document.getElementById('organicShare'), {
  type: 'line',
  data: {
    labels: ['Week 01','Week 02','Week 03','Week 04'],
    datasets: [
      { label: 'Organic (% by items)', data: [/* data */], tension: 0.3, borderColor: 'rgba(46, 125, 50, 1)' },
      { label: 'Organic (% by spend)', data: [/* data */], tension: 0.3, borderColor: 'rgba(129, 199, 132, 1)' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Organic share over time' } },
    scales: { y: { min: 0, max: 100, title: { display: true, text: 'Percentage (%)' } } }
  }
});

```

**ACCURACY AND BEHAVIOUR**

* Be conservative; ensure totals reconcile across all tables and graphs.
* Do not include any interpretation, judgement, or narrative.
* If a classification or organic status is uncertain and materially affects results, stop and ask for clarification.

```

```