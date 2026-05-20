---
layout: post
title:  "February 2026 Shopping Analysis"
date:   2026-02-21 00:00:00 +0000
categories: blog
history: 
location: High Halstow, Kent, UK
image: 
hide: true
---

Something new for 2026, I want to start showing some data visualisations of our shopping habits. This should then help see how we're aligned with our diet and spending goals. Aim is to keep us accountable and aligned with the direction of travel.

Before now getting to this level of data has been essentially impossible unless manually categorising everything from random paper receipts. However, we now shop at places with e-receipts which I can pump into my AI tool of choice to provide analysis for me based on defined prompts. Yes, this is incredibly obsessive and geeky, leave me alone. 

To help produce this, I use ChatGPT to process an input file (PDF or image) using [this prompt](/assets/random/data_extraction_categorisation_prompt.md), I ask it to process each receipt one by one, which allows me to manually validate categorisation and correct any mistakes. Once done, I combine into a master CSV for the month. I then ask ChatGPT to process that file using [this prompt](/assets/random/tables_charts_prompt.md) and provide tables for review and charts based on pre-defined templates. I've found this an interesting excercise in prompt engineering and using these tools. Generally, providing too much to do at once has led to inaccuracies and weirdness. Often the tools would wander and try to overachieve, despite clear boundaries. Processing more slowly and providing very specific and clear prompts has produced better outputs. 

I think we'll work on this through the year, and see what we can learn from the data. I genuinely have no idea what % of our shopping spend is meat vs vegetables, for example, so will be interesting to see.

This first graph I've tried to break down into somewhat relevant categories that will help us understand consumption patterns. For example, breaking down lentils/pulses, cheese and eggs into seperate categories.

Total spend for February 2026: XXXX

<!-- 1. Category Spend Stacked (Bar) -->
<div class="chart-wrap">
  <canvas id="categorySpendStacked"></canvas>
</div>

<script>
document.addEventListener("DOMContentLoaded", function () {

  const categorySpendData = {{ site.data.charts.category-spend | jsonify }};

  renderCategorySpendChart({
    element: "categorySpendStacked",
    year: "2026",
    weeks: ["05","06","07","08","09"],
    data: categorySpendData
  });

});
</script>

<style>
.chart-wrap{
  position: relative;
  width: 100%;
  height: 360px;
}
@media (max-width: 600px){
  .chart-wrap{ height: 520px; }
}
</style>

Categories look like this:
- **Fruit** – Fresh fruit eaten raw or used in meals and snacks, whether loose or packaged. This includes everyday and seasonal fruit. Dried fruit is excluded.
- **Vegetables (incl roots)** – Fresh cooking vegetables, including roots and non-leafy produce, plus fresh herbs used in cooking.
- **Salad & Leafy Greens** – Leafy and salad-style produce typically eaten raw or lightly dressed, including mixed salad bags and salad vegetables.
- **Meat & Fish** – Raw or minimally processed meat and fish.
- **Eggs** – The chicken kind, not the chocolate kind. 
- **Dairy** – Liquid and spoonable dairy products such as milk, yoghurt and cream. Butter is excluded.
- **Cheese** – Solid and soft cheeses bought as ingredients or standalone foods.
- **Bakery & Bread** – Bread and bakery staples such as loaves, wraps and baguettes.
- **Beans & Pulses** – Dried or tinned beans and pulses used as cooking staples. 
- **Ready Meals & Prepared** – Foods designed to be heated and eaten with little or no preparation. Kids ready meals, nuggets, fish fingers, pizza, quiche, etc.
- **Treats & Snacks** – Foods bought for enjoyment, including sweet and savoury snacks. Some healthy-ish, some not. 
- **Rice Pasta & Grains** – Dry grains and carbohydrates used as meal bases, including rice, pasta, couscous, oats and barley.
- **Dried Fruit & Nuts** – Shelf-stable dried fruit and nuts used for snacking or cooking. Mostly healthy.
- **Cupboard & Cooking** – Shelf-stable cooking ingredients and staples not usually eaten alone. Tinned tomatoes, sauces, condiments, stock, etc
- **Fats & Oils** – Cooking fats, including oils and butter.
- **Drinks** – Non-alcoholic drinks, cordials, teas, coffee, syrups, water, etc. Not alcohol.

Here's a breakdown of our spend across different shops by week (all weeks so far this year).

<canvas id="shopSpendByWeek"></canvas>
<script>
const totalsPlugin = {
  id: 'totalsPlugin',
  afterDatasetsDraw(chart) {
    const { ctx, scales: { x, y } } = chart;
    ctx.save();
    chart.data.labels.forEach((_, i) => {
      let total = 0;
      chart.data.datasets.forEach(ds => {
        total += ds.data[i] || 0;
      });
      const xPos = x.getPixelForTick(i);
      const yPos = y.getPixelForValue(total) - 8;
      ctx.fillStyle = '#333';
      ctx.font = 'bold 12px sans-serif';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'bottom';
      ctx.fillText(`£${total.toFixed(2)}`, xPos, yPos);
    });
    ctx.restore();
  }
};

new Chart(document.getElementById('shopSpendByWeek'), {
  type: 'bar',
  data: {
    labels: ['Week 01','Week 02','Week 03','Week 04','Week 05','Week 06','Week 07','Week 08','Week 09'],
    datasets: [
      { label: 'Ocado', data: [108.44,164.78,134.09,135.82,126.99,124.01,102.34,211.85,139.42], backgroundColor: '#6F2C91' },
      { label: 'Lidl', data: [16.99,13.32,12.08,4.81,0.00,0.00,0.00,0.00,0.00], backgroundColor: '#0050AA' },
      { label: 'M&S (store)', data: [0.00,13.28,0.00,5.18,34.85,20.55,0.00,22.85,0.00], backgroundColor: '#1F6A4D' },
      { label: 'Asda', data: [0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,22.48], backgroundColor: '#0077C8' },
      { label: 'Morrisons', data: [0.00,0.00,0.00,0.00,0.00,0.00,22.95,0.00,0.00], backgroundColor: '#4B9B3C' },
      { label: 'Sainsburys', data: [0.00,0.00,0.00,0.00,0.00,11.78,0.00,0.00,0.00], backgroundColor: '#F28C28' }
      // Add additional shops found in the data as additional datasets, each with Week 01–Week 09 values.
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Food spend by shop, by week' } },
    scales: { x: { stacked: true }, y: { stacked: true, title: { display: true, text: 'Spend (£)' } } }
  }
});

The major brands from Ocado are M&S and Ocado-own, so this shows the brand composition regardless of where we shop. The chart below reflects all weeks so far this year.

<canvas id="brandMix"></canvas>
<script>
new Chart(document.getElementById('brandMix'), {
  type: 'bar',
  data: {
    labels: ['M&S','Ocado','Other'],
    datasets: [{
      label: '% of spend',
      data: [52.28,9.77,37.95],
      backgroundColor: ['#1F6A4D','#6F2C91','#F28C28']
    }]
  },
  options: {
    plugins: { title: { display: true, text: 'Brand mix by spend (weeks 05–09)' } },
    scales: { y: { max: 100, title: { display: true, text: '%' } } }
  }
});
</script>

## Organic 

Organic share by category below is February only.

<canvas id="organicByCategory"></canvas>
<script>
new Chart(document.getElementById('organicByCategory'), {
  type: 'bar',
  data: {
    labels: ["Fruit","Salad & Leafy Greens","Vegetables","Meat & Fish","Dairy","Cheese","Rice Pasta & Grains","Bakery & Bread","Ready Meals & Prepared","Treats & Snacks","Cupboard & Cooking","Dried Fruit & Nuts","Fats & Oils","Eggs","Drinks","Beans & Pulses"],
    datasets: [
      { label: 'Organic', data: [34.69,59.26,52.94,40.00,61.76,57.14,0.00,21.43,20.00,9.09,5.26,14.29,0.00,66.67,21.05,33.33], backgroundColor: 'rgba(46, 125, 50, 0.75)' },
      { label: 'Non-organic', data: [65.31,40.74,47.06,60.00,38.24,42.86,100.00,78.57,80.00,90.91,94.74,85.71,100.00,33.33,78.95,66.67], backgroundColor: 'rgba(200, 200, 200, 0.7)' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Organic share by category (weeks 05–09, by item)' } },
    scales: { x: { stacked: true }, y: { stacked: true, max: 100, title: { display: true, text: '% of items' } } }
  }
});
</script>

Organic share over time below reflects all weeks so far this year.

<canvas id="organicShare"></canvas>
<script>
new Chart(document.getElementById('organicShare'), {
  type: 'line',
  data: {
    labels: ['Week 01','Week 02','Week 03','Week 04','Week 05','Week 06','Week 07','Week 08','Week 09'],
    datasets: [
      { label: 'Organic (% by items)', data: [5.97,8.64,2.99,45.00,20.78,31.82,36.73,54.35,25.64], tension: 0.3, borderColor: 'rgba(46, 125, 50, 1)' },
      { label: 'Organic (% by spend)', data: [10.01,11.57,4.82,58.93,39.08,28.94,50.08,60.82,43.74], tension: 0.3, borderColor: 'rgba(129, 199, 132, 1)' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Organic share over time' } },
    scales: { y: { min: 0, max: 100, title: { display: true, text: 'Percentage (%)' } } }
  }
});
</script>