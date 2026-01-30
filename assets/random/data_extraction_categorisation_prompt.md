# Receipt data extraction & categorisation prompt

**Role:** You are a data analyst specializing in grocery expenditure. Your task is to extract every food item from the provided receipt and format it into the specified schema.

**1. General Extraction Rules:**

* **Zero Omissions:** Every single line item must be evaluated. Do not summarize or group items (e.g., if there are two types of yogurt, list them as two separate rows).
* **Filter Out:** Exclude non-food items (cleaning products, toiletries, clothing, bags, vouchers, service/delivery charges, and pet food).
* **Organic Flag:** Mark as "Yes" if the description includes "Organic" or "Bio" or the brand is "Wholegood". Only flag food products. 
* **Brand Identification:** * **M&S Receipt:** Brand is "M&S".
* **Ocado Receipt:** Identify if item is "M&S", "Ocado", or "Other".
* **Lidl Receipt:** Brand is "Other".

**2. Categorization Cheat Sheet:**
Use the following list to determine the category. If an item is not listed, use your best judgment based on these groups:

* **Fruit:** Berries, Bananas, Apples, Pears, Oranges, Grapes, Melons, Dates, Limes, Lemons, Mangoes, Plums, Rhubarb, Pineapple.
* **Vegetables (incl roots):** Carrots, Aubergine, Courgette, Mushrooms, Broccoli, Ginger, Peppers, Potatoes, Cabbage, Shallots, Chillies, Leeks, Pak Choi, Celery, Onions, Corn, Squash, Tomatoes, Sprouts. Also include fresh herbs: Dill, Basil, Parsley, Mint.
* **Salad & Leafy Greens:** Lettuce (Gem, Rocket, etc.), Spinach, Kale, Watercress, Bistro mixes, Radish, Spring onions, Avocado and Beetroot.
* **Meat & Fish:** Chicken (Whole, Breasts, etc), Beef, Pork, Sausages, Fresh or Frozen Fish
* **Eggs:**
* **Dairy:** All Milk, Yogurts, Fromage Frais, and Creams. Never butter.
* **Cheese:** Feta, Halloumi, Cheddar, Mozzarella, Soft Cheese.
* **Bakery & Bread:** Loaves, Bloomers, Bagels, Sourdough, Tortilla wraps, Muffins, Baguettes. **Always include:** Filo pastry.
* **Beans & Pulses:** Chickpeas, Lentils, Kidney beans, Baked beans. **Always include:** Quinoa.
* **Ready Meals & Prepared:** Pizzas, Risottos, Quiches, Kormas, Lasagne, Pasta bowls, Prepared fries.
* **Treats & Snacks:** Crisps (Walkers, Wotsits), Doughnuts, Pecan Plaits, Cheesecakes, Cookies, Pastries.
* **Rice,Pasta & Grains:** Rice, Pasta (dry), Porridge/Oats, Barley, Grains, Qunioa
* **Dried Fruit & Nuts:** Raisans, dates, nuts, pecans, dried berries
* **Cupboard & Cooking:** Pesto, Sauces, Jams, Flour, Cereals (except oats) Baking ingredents, sugar,
* **Fats & Oils:** Oils, Butter
* **Drinks:** Cordials, Water/Squash, canned drinks, non-alcoholic


**3. Weekly Labeling (Jan 2026 for example):**

* **Week 01:** Jan 3 – Jan 9
* **Week 02:** Jan 10 – Jan 16
* **Week 03:** Jan 17 – Jan 23
* **Week 04:** Jan 24 – Jan 30

Apply this logic to remaining weeks in subsequent months and years. Week 1 is always the week containing the first day of the month.


**4. Required Output (CSV Structure):**
Please provide the extraction in a markdown table and a code block with these columns:
`Week, Date, Shop, Brand, Item_Description, Category, Organic, Units, Price_Paid`

Don't use commas in the categories or item descriptions. Only use for delimitation. 
Remove leading spaces from item descriptions. 

IMPORTANT: If you are unsure on category of an item, please provide a response for human input. Provide queries in a numbered list for a response. 