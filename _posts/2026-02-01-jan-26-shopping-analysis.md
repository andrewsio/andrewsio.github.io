---
layout: post
title:  "January 2026 Shopping Analysis"
date:   2026-01-31 00:00:00 +0000
categories: blog
history: 
location: High Halstow, Kent, UK
image: 
---
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

Something new for 2026, I want to start showing some data visualisations of our shopping habits. This should then help see how we're aligned with our diet and spending goals. Aim is to keep us accountable and aligned with the direction of travel.

Before now getting to this level of data has been essentially impossible unless manually categorising everything from random paper receipts. However, we now shop at places with e-receipts which I can pump into my AI tool of choice to provide analysis for me based on defined prompts. Yes, this is incredibly obsessive and geeky, leave me alone. 

To help produce this, I use ChatGPT to process an input file (PDF or image) using [this prompt](/assets/random/data_extraction_categorisation_prompt.md), I ask it to process each receipt one by one, which allows me to manually validate categorisation and correct any mistakes. Once done, I combine into a master CSV for the month. I then ask ChatGPT to process that file using [this prompt](/assets/random/tables_charts_prompt.md) and provide tables for review and charts based on pre-defined templates. I've found this an interesting excercise in prompt engineering and using these tools. Generally, providing too much to do at once has led to inaccuracies and weirdness. Often the tools would wander and try to overachieve, despite clear boundaries. Processing more slowly and providing very specific and clear prompts has produced better outputs. 

I think we'll work on this through the year, and see what we can learn from the data. I genuinely have no idea what % of our shopping spend is meat vs vegetables, for example, so will be interesting to see.

This first graph I've tried to break down into somewhat relevant categories that will help us understand consumption patterns. For example, breaking down lentils/pulses, cheese and eggs into seperate categories. Actually quite surprising already how much we spend on things like vegetables vs Treats & Snacks, although we have been exceptionally healthy this month, so that may be why.

Total spend for January 2026: £608.79

<div class="chart-wrap">
  <canvas id="categorySpendStacked"></canvas>
</div>

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

<script>
const ctx = document.getElementById('categorySpendStacked');

new Chart(ctx, {
  type: 'bar',
  data: {
    labels: ['Bakery & Bread','Beans & Pulses','Cheese','Cupboard & Cooking','Dairy','Dried Fruit & Nuts','Drinks','Eggs','Fats & Oils','Fruit','Meat & Fish','Ready Meals & Prepared','Rice Pasta & Grains','Salad & Leafy Greens','Treats & Snacks','Vegetables'],
    datasets: [
      { label: 'Week 01', data: [4.30,2.42,0,10.55,11.99,8.75,8.05,3.25,2.80,30.15,3.49,7.60,0,10.02,3.25,18.81] },
      { label: 'Week 02', data: [13.93,2.48,8.99,11.65,10.50,17.75,18.95,3.30,0,20.06,13.75,11.60,9.54,11.65,6.45,30.78] },
      { label: 'Week 03', data: [4.44,5.15,7.19,1.00,10.15,12.50,6.30,2.80,0,24.58,22.79,13.05,0,12.45,0,23.77] },
      { label: 'Week 04', data: [3.48,0,6.80,3.20,15.20,16.95,0,6.00,1.75,11.91,27.12,5.68,0,13.35,6.99,27.38] }
    ]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,   // key: honour the wrapper height
    layout: { padding: { top: 8, right: 8, bottom: 8, left: 8 } },
    plugins: {
      title: { display: true, text: 'Monthly spend by category (stacked by week)' },
      legend: {
        position: 'bottom',
        labels: { boxWidth: 10 }
      },
      tooltip: { mode: 'index', intersect: false }
    },
    interaction: { mode: 'index', intersect: false },
    scales: {
      x: {
        stacked: true,
        ticks: {
          autoSkip: true,
          maxRotation: 60,
          minRotation: 60,
          padding: 6
        }
      },
      y: {
        stacked: true,
        title: { display: true, text: 'Spend (£)' },
        ticks: { callback: (v) => '£' + v }
      }
    }
  }
});

window.addEventListener('orientationchange', () => Chart.getChart(ctx)?.resize());
</script>

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

Here's a breakdown of our spend across different shops by week. We're trying to focus on Ocado as our big weekly shop. We have the delivery saver, so want to make use of it. We have been using Lidl for top-up shops and a little bit of M&S here and there, usually when it's convenient. We also shop at Costco, but that's usually a quarterly visit. We'll need to add that in here at some point. 

Sticking to a weekly meal plan should help narrow our shopping habits as in years past we tend to freestyle and go wherever and whenever and generally not having a structured plan. Not a good idea. 

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
    labels: ['Week 01','Week 02','Week 03','Week 04'],
    datasets: [
      { label: 'Ocado', data: [108.44,164.78,134.09,135.82], backgroundColor: '#6F2C91' },
      { label: 'Lidl', data: [16.99,13.32,12.08,4.81], backgroundColor: '#0050AA' },
      { label: 'M&S (store)', data: [0,13.28,0,5.18], backgroundColor: '#1F6A4D' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Food spend by shop, by week' } },
    scales: { x: { stacked: true }, y: { stacked: true, title: { display: true, text: 'Spend (£)' } } }
  }
});
</script>

The major brands from Ocado are M&S and Ocado-own, so this shows the brand composition regardless of where we shop. Generally we've found M&S branded to be better than Ocado although Ocado is almost always a little cheaper. For example, milk is usually 10 or 20p cheaper for the Ocado brand.

<canvas id="brandMix"></canvas>
<script>
new Chart(document.getElementById('brandMix'), {
  type: 'bar',
  data: {
    labels: ['M&S','Ocado','Other'],
    datasets: [{
      label: '% of spend',
      data: [56.66,12.92,30.41],
      backgroundColor: ['#1F6A4D','#6F2C91','#F28C28']
    }]
  },
  options: {
    plugins: { title: { display: true, text: 'Brand mix by spend' } },
    scales: { y: { max: 100, title: { display: true, text: '%' } } }
  }
});
</script>

## Organic 

One of our annual goals is to eat more organic food. It's surprisingly difficult in the UK to get a good variety of organic. As you can see from the chart, we (I, lol) conducted a bit of an experiment in Week 4. I think a good excercise, it was certainly possible to switch but the range does has it's limits. Some items were noticably better in quality, the chicken although expenisve was very, very good and the apples, salad and tomatoes were much tastier. All a lot more expensive though. The Milk, Eggs and Yoghurt we found to be comparable, but I think the main benefit there is welfare standards. I don't think a 50% Organic composition weekly is achievable yet so we need to warm into it more slowly. It is psychologically challenging to pick the more expensive option when the label appears to be the only visual difference. 

For Feburary, I think we'll commit to Organic is specific areas. Dairy and cheese seems to be a practical starting place, as the price jump isn't too large. On that, I was pleasantly surprised to see that the supplied milk at work is Organic. Go Colliers! Eggs is another option, although the jump from ~25p to ~50p an egg is quite a jump. 

<canvas id="organicByCategory"></canvas>
<script>
new Chart(document.getElementById('organicByCategory'), {
  type: 'bar',
  data: {
    labels: ['Bakery & Bread','Beans & Pulses','Cheese','Cupboard & Cooking','Dairy','Dried Fruit & Nuts','Drinks','Eggs','Fats & Oils','Fruit','Meat & Fish','Ready Meals & Prepared','Rice Pasta & Grains','Salad & Leafy Greens','Treats & Snacks','Vegetables'],
    datasets: [
      { label: 'Organic', data: [28.57,7.14,10,27.27,12.5,23.08,25,40,0,9.52,14.29,0,40,20.69,12.5,9.72], backgroundColor: 'rgba(46, 125, 50, 0.75)' },
      { label: 'Non-organic', data: [71.43,92.86,90,72.73,87.5,76.92,75,60,100,90.48,85.71,100,60,79.31,87.5,90.28], backgroundColor: 'rgba(200, 200, 200, 0.7)' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Organic share by category (monthly, by item)' } },
    scales: { x: { stacked: true }, y: { stacked: true, max: 100, title: { display: true, text: '% of items' } } }
  }
});
</script>

<canvas id="organicShare"></canvas>
<script>
new Chart(document.getElementById('organicShare'), {
  type: 'line',
  data: {
    labels: ['Week 01','Week 02','Week 03','Week 04'],
    datasets: [
      { label: 'Organic (% by items)', data: [6.67,9.59,3.33,43.40], tension: 0.3, borderColor: 'rgba(46, 125, 50, 1)' },
      { label: 'Organic (% by spend)', data: [10.01,11.57,4.82,58.93], tension: 0.3, borderColor: 'rgba(129, 199, 132, 1)' }
    ]
  },
  options: {
    plugins: { title: { display: true, text: 'Organic share over time' } },
    scales: { y: { min: 0, max: 100, title: { display: true, text: 'Percentage (%)' } } }
  }
});
</script>