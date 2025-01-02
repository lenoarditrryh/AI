# How to Scrape Google Maps Search Results Using Nstbrowser RPA Tool

Leveraging RPA tools for web data scraping has become a common method for data collection. These tools can significantly improve efficiency while reducing costs. **[Nstbrowser RPA](https://www.nstbrowser.io/zh/rpa)** provides an excellent user experience and maximizes productivity for such tasks.

---

## What You Will Learn:

- How to use RPA for data collection.
- How to save the data collected through RPA.

---

## Step 1: Preparation

To begin, you need an Nstbrowser account. Log in to the **[Nstbrowser client](https://app.nstbrowser.io/account/login)**, navigate to the RPA module, and create a new workflow.

You are now ready to set up a workflow for scraping Google Maps search results.

---

## Step 2: Access the Target Website

Before searching for the target content, you need to visit the target website: **[Google Maps](https://www.google.com/maps)**.

Use the `Goto Url` node to configure the website URL, enabling you to access the target site.

![Goto Url Node](https://assets.nstbrowser.io/prod/posts/91ur4W0MR0z8-d2b5ca33bd970f64a6301fa75ae2eb22.png)

---

## Step 3: Search for Target Content

Once you've reached the target website, you'll need to search for your desired address or location. Use **[Chrome DevTools](https://leeon.gitbooks.io/devtools/content/learn_basic/overview.html)** to locate HTML elements.

### Using DevTools

1. Open DevTools and inspect the search bar.
2. Identify the `id` attribute for the input field, which will serve as the CSS selector for element targeting.

### Input Search Content

- Add an `Input Content` node:
  - Set **Element** to `Selector`.
  - Enter the `id` value of the input field in the selector.
  - Input the desired search term under **Content**.

![Input Content Node](https://assets.nstbrowser.io/prod/posts/yVkfaMYlE0fU-d2b5ca33bd970f64a6301fa75ae2eb22.png)

### Simulate Search Action

Use the `Keyboard` node to simulate a keyboard press (e.g., Enter key) and execute the search.

![Keyboard Node](https://assets.nstbrowser.io/prod/posts/iMJBeTMuDtIV-d2b5ca33bd970f64a6301fa75ae2eb22.png)

---

## Step 4: Scrape the Data

Once you've conducted your search, the search results will appear as a list. Google Maps presents results in a classic list format, with important details displayed in the list and additional information shown upon selecting an item.

![Google Maps List View](https://assets.nstbrowser.io/prod/posts/TnBnieaQlXhw-d2b5ca33bd970f64a6301fa75ae2eb22.png)

### Iterate Through the Results

Use a `Loop Element` node to iterate through all the results in the list. Save each element in a `map` variable and its index in a `map-index` variable for further processing.

![Loop Element Node](https://assets.nstbrowser.io/prod/posts/1SqcZotl75Ht-d2b5ca33bd970f64a6301fa75ae2eb22.png)

Add a wait action (`Wait Time` or `Wait Request`) before the loop to ensure that all elements are fully loaded before scraping.

---

## Step 5: Click Each List Item

Within the loop, use the `Get Element Data` node to locate clickable elements based on the `map` variable. Then, use the `Click Element` node to select each item.

![Click Element Node](https://assets.nstbrowser.io/prod/posts/I0aubG5uYX7S-d2b5ca33bd970f64a6301fa75ae2eb22.png)

---

## Step 6: Extract Data

After clicking each list item, use the `Get Element Data` node to extract detailed information about the selected result. Save the data into a predefined table for organization.

![Get Element Data Node](https://assets.nstbrowser.io/prod/posts/vWqtoJh8Rtvj-d2b5ca33bd970f64a6301fa75ae2eb22.png)

---

## Step 7: Repeat Actions

For broader data collection, you may need to repeat the process multiple times. Use the `Repeat Flow` node to repeat the scraping workflow based on the desired number of iterations or a specified condition.

![Repeat Flow Node](https://assets.nstbrowser.io/prod/posts/XzyjkOv3gS0A-d2b5ca33bd970f64a6301fa75ae2eb22.png)

---

## Step 8: Save the Results

Once all the required data is collected, save it for further analysis. **Nstbrowser RPA** offers two saving options:

1. `Save To File`
2. `Save To Excel`

For convenience, choose `Save To Excel`. Configure the file path, file name, and content to save your data efficiently.

![Save To Excel Node](https://assets.nstbrowser.io/prod/posts/cQEevp3yQHZG-d2b5ca33bd970f64a6301fa75ae2eb22.png)

---

## Step 9: Execute the Workflow

Save your configured workflow, create a scheduled task, and click the run button to start collecting data from Google Maps.

![Executing Workflow](https://assets.nstbrowser.io/prod/posts/VFuWQhtRSBQp-f73700c48abd01366d065394ec8d3d4b.gif)

---

## Conclusion

By configuring the workflow once, you can automate your data scraping process and repeat it anytime with ease. This demonstrates the power and efficiency of **Nstbrowser RPA** for Google Maps data scraping.

### Get Started with Nstbrowser RPA!

The Google Maps scraping feature is now available in the **[Nstbrowser RPA marketplace](https://www.nstbrowser.io/zh/rpa/marketplace)**. Download the workflow, customize the search content and file paths, and start your RPA data scraping journey today!

![Nstbrowser RPA](https://assets.nstbrowser.io/prod/posts/f1DlFfgvmZpR-d2b5ca33bd970f64a6301fa75ae2eb22.png)
