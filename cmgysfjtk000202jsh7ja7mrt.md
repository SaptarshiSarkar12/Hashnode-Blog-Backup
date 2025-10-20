---
title: "Mastering Data Cleanup: Unleash the Power of OpenRefine"
seoTitle: "OpenRefine: Master Data Cleanup Easily"
seoDescription: "Learn to clean messy data using OpenRefine. Transform, standardize, and export tidy datasets ready for visualization with this practical guide"
datePublished: Mon Oct 20 2025 07:02:12 GMT+0000 (Coordinated Universal Time)
cuid: cmgysfjtk000202jsh7ja7mrt
slug: mastering-data-cleanup-unleash-the-power-of-openrefine
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1760942022801/1f1fe6a7-fb55-457c-8cb2-54119d32954b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1760942218982/3c2ac33f-0f9f-4798-be63-3bff816a45a9.png
tags: data-visualization, data-cleaning, data-wrangling, openrefine, handsonlearning, grel

---

Real-world data is messy. It has inconsistent spellings, stray characters, and mixed number formats, which can cause problems even with simple analysis. In this post, I will guide you through a practical, beginner-friendly OpenRefine workflow (based on an example from the **Hands-On Data Visualization** book) to clean a small but intentionally messy sample dataset. By the end, you'll be able to convert noisy numeric fields into proper numbers, cluster and standardize text values, and export a tidy CSV ready for visualization.

## Prerequisites

You'll need the following tools and files ready before you start the walkthrough:

* Latest version of [OpenRefine](https://openrefine.org/download) installed
    
* Downloaded CSV file of the [sample messy data](https://docs.google.com/spreadsheets/d/19BilYJxd0fgi7MTAa2y9NUF65Xqf2_y_dVr1jPbmWeg/) provided in the [**Hands-On Data Visualization** book](https://handsondataviz.org/open-refine.html#open-refine)
    

## Dataset preview

Before we start cleaning, let’s look at what the raw data actually looks like. The screenshot below shows the first 10 rows of the sample dataset. Notice the inconsistent spellings in the `Country` column and the mix of symbols and commas in `FundingAmount` column — we’ll fix all of these with OpenRefine.

![A spreadsheet titled "Sample Messy US Foreign Aid Data" shows data for different years, countries, funding agencies, and funding amounts. Some country names and agency names are inconsistent, and funding amounts vary in format.](https://cdn.hashnode.com/res/hashnode/image/upload/v1760833887607/e387f6eb-5025-4ec7-9ec3-2441dbc714ee.png align="center")

## Data Cleaning

Now that we’ve explored the dataset, let’s start cleaning it using **OpenRefine**. In this section, we’ll walk through a few essential steps to turn messy, inconsistent data into a tidy and analysis-ready table. We’ll begin by importing the CSV into OpenRefine, then clean up numeric fields, standardize text values, and finally export a clean version of the dataset.

OpenRefine lets you make these transformations interactively, with instant previews and the ability to undo or redo any step — perfect for exploring and cleaning data safely before analysis.

### Step 1: Importing and parsing (Creating a new project)

1. Start the **OpenRefine** application. You should see a webpage open like this:
    
    ![Screenshot of the OpenRefine application interface](https://cdn.hashnode.com/res/hashnode/image/upload/v1760835936172/907fd7cb-d044-4665-91ca-eff78b3c6f0e.png align="center")
    
2. Since we have already downloaded the **CSV** file of the dataset, we will upload it from our local computer. Click on **This Computer** → **Choose Files** to upload our dataset. You can also drag and drop the file there.
    
    ![Screenshot showing that the data file has been chosen](https://cdn.hashnode.com/res/hashnode/image/upload/v1760836246518/9963168f-3172-41d3-8db9-60c996a143c5.png align="center")
    
3. Click on **Next**. This will show the progress of the data upload.
    
    ![uploading data in progress](https://cdn.hashnode.com/res/hashnode/image/upload/v1760836347325/1ae53217-b2f6-45e8-a782-0900a0c3337a.png align="center")
    
4. Finally, our dataset is parsed and previewed. Make sure the data is displayed correctly here. If everything looks good, proceed with creating the project by clicking the **Create project** button.
    
    ![Screenshot of the OpenRefine interface when the dataset is parsed properly](https://cdn.hashnode.com/res/hashnode/image/upload/v1760836416458/addf15bb-057c-4db9-af56-6870773715d7.png align="center")
    
5. The project will open and look like this. Since there are 127 rows and only 10 are shown, we'll switch to display all of them by clicking the "500 rows" button. This gives us a complete view of the data for proper analysis and cleaning.
    
    ![Screenshot of OpenRefine interface showing the complete dataset uploaded](https://cdn.hashnode.com/res/hashnode/image/upload/v1760836936412/27ab5920-c6fb-4dc1-9de6-81f135719186.png align="center")
    

### Step 2: Clean numeric column (`FundingAmount`)

Generally, we can use **facets** to highlight differences in large datasets because manually analyzing each cell for deviations from the expected result is time-consuming. Since the `FundingAmount` column should contain positive numbers, we can apply a **Custom text facet** to identify **non-numeric cells**.

![Screenshot of how to navigate to "Custom text facet" option](https://cdn.hashnode.com/res/hashnode/image/upload/v1760841012497/eb4d8b7a-c3b0-4b27-a7dd-bbb27df26d79.png align="center")

We will need to reduce the whole data set into a smaller data set excluding those that can be converted to positive numbers (numeric datatype). So, we’ll be using the below [**GREL**](https://openrefine.org/docs/manual/grel) expression to classify the dataset into two groups — **Valid** and **Invalid** based on whether the values can be converted to a **positive number**.

```excel
if(
    isError(value.toNumber()),
    "Invalid",
    if(
        value.toNumber() < 0,
        "Invalid",
        "Valid"
    )
)
```

![Screenshot of the custom facet we're setting](https://cdn.hashnode.com/res/hashnode/image/upload/v1760885792572/54d58bce-d4fa-4b6e-bfba-d4cb0042babd.png align="center")

Here is what each part of the expression means:

* `toNumber()` function - converts the value to a number (first, the value is converted to a string if it's not already in string format, and then to a number)
    
* `isError()` function - Takes a GREL expression as input and returns true if the expression results in an error, and false otherwise.
    
* `if()` function - Takes three arguments in this order: the expression to evaluate, what to return if true, and what to return if false.
    

We will categorize the entire dataset into two groups:

* **Valid**: if the value can be successfully converted to a positive number
    
* **Invalid**: if the value cannot be converted to a number or if the converted number is negative
    

Click on `Ok` to apply the facet, and we’ll see two choices: **Valid** and **Invalid**. We’ll `include` only the data records labeled as **Invalid**. Now, the number of rows decreases from **127** to **121** — not a huge reduction, but it helps in focusing on the problematic entries.

![Screenshot showing the applied facet](https://cdn.hashnode.com/res/hashnode/image/upload/v1760886254872/5638b68b-982a-40f7-b6c4-3ae637fffdb6.png align="center")

![Screenshot showing some of the matching rows on applying the facet](https://cdn.hashnode.com/res/hashnode/image/upload/v1760886648898/9ac93efe-70df-45e8-b07a-88ae5c968df4.png align="center")

Now, we’ll procced with transforming the invalid values by removing redundant commas and spaces, dollar sign, etc.

1. Click on `Edit cells` and then on `Transform` option in the `FundingAmount` column.
    
    ![Screenshot of how to navigate to "Transform" option](https://cdn.hashnode.com/res/hashnode/image/upload/v1760887357826/422f6b78-8447-47d7-94ac-f596f6b1b3c3.png align="center")
    
2. We will now replace the commas, spaces, dollar signs, and any unnecessary characters in the number. The following GREL expression will be used:
    
    ```cpp
    value.replace(/[a-z$, ]/, "")
    ```
    
    The regex expression `[a-z$, ]` matches any lowercase letters, dollar signs, commas, and spaces. The `replace()` function will replace each of these matches with an empty string.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760888368665/68e9c1c0-c391-4c86-8d47-d19825063651.png align="center")
    
3. On applying the transformation, we’ll see that a large part of our dataset has got cleaned. As we have selected only **invalid** group, only the records containing negative numbers are shown.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760889208912/4e1283bf-4d09-43d1-a9aa-6d8ac9c29709.png align="center")
    
4. We’ll now finally convert the negative numbers to positive ones using the following GREL expression for the transformation:
    
    ```cpp
    value.toNumber() * -1
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760889633393/e93a8eea-4480-40b0-a72b-06104be7b8bd.png align="center")
    
    As soon as we apply the transformation, all the values in the `FundingAmount` column have been converted to positive numbers. Now, we’ll remove the facet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760889724179/25f1a2e9-3a7d-4ce7-a68c-223a973cab6c.png align="center")
    
    Finally, we’ll convert each of the values to `Number` format using `Edit cells` → `Common transforms` → `To number` option.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760935695235/c4fa5594-5bb1-4f99-97a1-be49d15fc190.png align="center")
    

### Step 3: Standardizing text column (`Country` & `FundingAgency`)

The `Country` column contains inconsistent spellings and variations of “North Korea” and “South Korea”. Similar cases are also observed in the `FundingAgency` column.  
One of the most powerful features of OpenRefine is [**clustering**](https://openrefine.org/docs/manual/cellediting#cluster-and-edit) which find groups of cell values containing the alternative representation of the same thing.

1. Click on the **arrow-down button** of the `Country` column → `Edit Cells` → `Cluster and edit` option.
    
    ![Screenshot of OpenRefine interface showing how to navigate to "Cluster and edit" option](https://cdn.hashnode.com/res/hashnode/image/upload/v1760930464794/64a963e2-a882-4279-8335-eabf87c20531.png align="center")
    
    ![Screenshot of OpenRefine's Cluster and edit window](https://cdn.hashnode.com/res/hashnode/image/upload/v1760930613528/579826da-fe99-4d49-a441-2a702761e7fb.png align="center")
    
    We're using the default [**clustering method**](https://openrefine.org/docs/manual/cellediting#clustering-methods). You can learn more about each of the [clustering methods in OpenRefine’s documentation](https://openrefine.org/docs/technical-reference/clustering-in-depth).
    
2. We’ll set the new cell value to `North Korea` and `South Korea` accordingly. Finally, we’ll click on `Merge selected & Close` option.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760931448277/19e5bd6f-62af-4d17-9496-eb6a1d56b660.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760931558280/7ca042c9-f7ed-4bea-9494-712b68570ba0.png align="center")
    
3. Let’s check if any cells have value other than `North korea` and `South Korea`. We’ll use the following **GREL** expression for our custom facet to categorize the cell values into **Valid** and **Invalid** groups.
    
    ```excel
    if ((value == "North Korea").or(value == "South Korea"),
        "Valid",
        "Invalid"
    )
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760932053933/8acbb1de-4be8-4a1a-a080-da170aea501f.png align="center")
    
4. We’ll select the **Invalid** choice in facet. We can see that 3 cell values need cleaning.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760932167200/b97766a4-52ad-44e4-86f6-cfeef6299b9f.png align="center")
    
5. We'll first replace `Nor` and `xNorth` with `North` so we can use clustering, which is a better method than editing each cell directly, especially for a large number of rows.
    
    The following **GREL** expression will be used:
    
    ```c
    value.replace(", Nor", " North")
         .replace("xNorth", "North")
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760932751478/42a6daf8-d76e-4c3b-a0cf-1cc1c0b89d01.png align="center")
    
6. We’ll first remove the facet because we need to apply clustering to the entire dataset to find similarities. Then, we’ll select the `Cluster and edit` option and choose the [**n-Gram fingerprint**](https://openrefine.org/docs/technical-reference/clustering-in-depth#n-gram-fingerprint) method with an **n-Gram** size of 1. We’re choosing the n-Gram fingerprint method because the only difference between `South Korea` and `SouthKorea` is a space, and the n-Gram fingerprint method removes **all** spaces.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760934783791/28d06864-ceeb-40aa-8292-67181b2c43ea.png align="center")
    
    Now, we’ll merge those two clusters.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760935056230/65ca0c51-58e4-4d66-a958-b3fe6b1d6fd1.png align="center")
    

We have now successfully cleaned the `Country` column.

Similarly, for the `FundingAgency` column, we’ll apply **n-Gram Fingerprint** clustering method with **n-Gram size** as **1**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760936256103/4d4eae8f-dba9-44c9-859c-9b57ceaaefe0.png align="center")

This clustering method can sometimes produce false positives, so be sure to check the cluster values before merging. Notice that in the second cluster, **Department of Defense** is included in the *cluster* of **Department of State**, which is incorrect. Therefore, we’ll leave the **Department of Defense** value **unchecked** while merging.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760936482675/b4991ca4-3179-405d-8a2f-f9db1a40a1f6.png align="center")

Using `Text facet`, we can view the different groups of values in that column. We notice that some values are still messy, like `Department - Agriculture` and `U.S. Agency: International Development`. So, we’ll use clustering again. This time, we’ll use the [**Nearest neighbor** clustering method](https://openrefine.org/docs/technical-reference/clustering-in-depth#nearest-neighbor-methods) (with the [**PPM** function](https://openrefine.org/docs/technical-reference/clustering-in-depth#ppm)) because the cell values share some common words, making it helpful to find the nearest neighbor in this case.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760937058810/bc04fec4-7f4b-43e7-9c71-d247193084d8.png align="center")

We’ll now merge these three clusters. Next, try increasing the radius value to find more nearest neighbors to catch messy data values with slight similarities (like `Department of Argic` and `Department of Agriculture`).  
I tried setting the radius value to `3.0` and found some correct clusters that I considered merging.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760937627040/78415736-2513-47ab-9ea8-8513d38d463d.png align="center")

## Step 4: Quick sanity checks & facets

To verify whether the complete dataset has been cleaned, we can use the following facets:

* `Numeric facet` on `Funding Amount` column
    
* `Text facet` on `Country` and `FundingAgency` columns
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760938045124/27ec8f34-7bf9-46a2-89ff-bd06097e71f6.png align="center")

Upon examining the facets, we see that they are all valid. Therefore, we have successfully cleaned the dataset.

**Congratulations on cleaning your *first* dataset!**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760938401507/5a198622-9c7a-4651-94bf-3f9a06ff2e27.gif align="center")

## Export & reproducibility

You can now export the cleaned dataset into a file (like **CSV**) or to a database (such as **SQL**).  
To export, click on the **Export** button in the top right corner. I am choosing **CSV** as the output file type.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760939891684/b65077a4-2530-4529-8de1-7ec634ae9a10.png align="center")

## **Conclusion**

Data cleaning is often the most time-consuming part of data analysis. With **OpenRefine**, you can make this step both reproducible and efficient.

#### **Acknowledgments & References**

This walkthrough was inspired by the *Hands-On Data Visualization* book by **Jack Dougherty** and **Ilya Ilyankou**, which provides the sample dataset and a concise introduction to cleaning data with OpenRefine.

For detailed explanations of **OpenRefine’s** features, transformations, and architecture, refer to the official [OpenRefine Documentation](https://openrefine.org/docs).

Both the book and the documentation are excellent resources if you’d like to explore more advanced data-cleaning techniques and reproducible workflows.

#### **Resources**

* *Hands-On Data Visualization* — [https://handsondataviz.org](https://handsondataviz.org)
    
* *OpenRefine Official Documentation* — [https://openrefine.org/docs](https://openrefine.org/docs)
    

I learned a lot by following the *Hands-On Data Visualization* example and exploring **OpenRefine’s** documentation. If you’re just starting out with data cleaning, these two resources are the perfect next step.

You can also view my cleaned dataset here: [Cleaned dataset on Google Sheets](https://docs.google.com/spreadsheets/d/1TIDDG9WlPJky2_vqgFmyu2DxkZ4_m0w-4E33A8JU458/edit?usp=sharing)