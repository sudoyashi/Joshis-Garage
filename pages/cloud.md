---
layout: page
title: Cloud Computing
permalink: /cloud/
---

## Work in the Cloud industry

My cloud WIP resume website, via Azure: [Cloud Resume](https://cloudresume619.z22.web.core.windows.net/)

I've worked on and off in IT for about 4 years now and in that time, I've learned enough to feel confident to step up to work in cloud computing. Cloud computing is a technology that I believe most, if not all, companies should invest in. Cloud is not a new idea, but the implementation to reap the benefits is where the transition for most businesses are struggling.

It's not intuitive technology to work with and seasoned on-prem professionals may not find the need to  still untapped potential because it's fundamentally different than how you would treat a physical machine. The ideas behind the computer setup are not different, but the provisioning, licensing, price optimization, decisions between storage modes, and so on is the new challenge with cloud.

I'm going through [The Cloud Resume Challenge](https://cloudresumechallenge.dev/docs/the-challenge/azure/) to learn more about Cloud computing to eventually become a Cloud Solutions Architect or Cloud Engineer.

## Starting goal: Complete The Cloud Resume Challenge

Based on [The Cloud Resume Challenge for Azure](https://cloudresumechallenge.dev/docs/the-challenge/azure/), my goal is to complete these 16 steps to learn and show what I can do with Azure.

Checklist:

- [x] 1. Certification
- [x] 2. HTML
- [x] 3. CSS
- [x] 4. Static Website
- [x] 5. HTTPS
- [ ] 6. DNS
- [x] 7. Javascript
- [ ] 8. Database
- [ ] 9. API
- [ ] 10. Python
- [ ] 11. Tests
- [ ] 12. Infrastructure as Code
- [ ] 13. Source Control
- [ ] 14. CI/CD (Back end)
- [ ] 15. CI/CD (Front end)
- [ ] 16. Blog post

### 1. Certification - DONE

Your resume needs to have the AZ-900 certification on it. This is an introductory certification that orients you on the Azure cloud – if you have a more advanced Azure cert, that’s fine but not expected. You can sit this exam online for $100 USD. A Cloud Guru offers exam prep resources.

[AZ-900 received on June 10, 2023](https://www.credly.com/badges/0c8be48a-c34a-45af-bc69-1f6a8ca1acbb/public_url)

<div data-iframe-width="150" data-iframe-height="270" data-share-badge-id="0c8be48a-c34a-45af-bc69-1f6a8ca1acbb" data-share-badge-host="https://www.credly.com"></div><script type="text/javascript" async src="//cdn.credly.com/assets/utilities/embed.js"></script>

### 2. HTML

Your resume needs to be written in HTML. Not a Word doc, not a PDF. Here is an example of what I mean.

HTML seems to be fine. Using a template from [StyleShout](https://styleshout.com/free-templates/ceevee/). Why use a template? The amount of time saved from reinventing a custom HTML site isn't the main goal, it's to deploy a static website on Azure. There are TONS of resources that are already made so that you don't have to speend time making everything from scratch.

- *Status: Started 6/19/2023, 5:06PM*

### 3. CSS

Your resume needs to be styled with CSS. No worries if you’re not a designer – neither am I. It doesn’t have to be fancy. But we need to see something other than raw HTML when we open the webpage.

Same with HTML, less effort in modifying existing code than to remake everything on your own. Again, save time from doing the general tasks and focus on the ones that we need to do: deploy a static website on Azure.

- *Status: Started 6/19/2023, 5:06PM*

### 4. Static Website

Your HTML resume should be deployed online as an Azure Storage static website. Services like Netlify and GitHub Pages are great and I would normally recommend them for personal static site deployments, but they make things a little too abstract for our purposes here. Use Azure Storage.

Following the guide from Microsoft: [Host a static website in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website-how-to?tabs=azure-portal) using Powershell.

```powershell
# Login to Azure
Connect-AzAccount

# Setup new rg, if does not exist already
$resourceGroup = 'cloud-resume'
$location = "westus"
$storageAccount = "cloudresume619"
az account set --subscription 'Training subscription'
az group list -otable
az group create --name $resourceGroup --location $location --tags "Env=dev"

# Setup storage account

az storage account create `
--name $storageAccount `
--resource-group $resourceGroup `
--location $location `
--sku Standard_LRS `
--kind StorageV2


# Enable static web hosing
az storage blob service-properties update `
--account-name $storageAccount `
--static-website `
--404-document "404.html" `
--index-document "index.html"

# Navigate to website files root directory if needed
az storage blob upload-batch -s "C:\Users\joshu\Documents\git\cloud-resume\" -d '$web' --account-name $storageAccount

# Print public URL
az storage account show -n $storageAccount `
-g $resourceGroup `
--query "primaryEndpoints.web" `
--output tsv

# Setup metrics
az monitor metrics 
```

Visit the current site here: [Cloud Static Website](https://cloudresume619.z22.web.core.windows.net/)

- *Status: Started 6/19/2023 8:12PM*

### 5. HTTPS

The Azure Storage website URL should use HTTPS for security. You will need to use Azure CDN to help with this.

The official website (link above) is HTTPS secured!

- *Status: 6/19/2023 10:37PMs.*

### 6. DNS

Point a custom DNS domain name to the Azure CDN endpoint, so your resume can be accessed at something like my-c00l-resume-website.com. You can use Azure DNS or any other DNS provider for this. A domain name usually costs about ten bucks to register.

I'll purchase this in a bit.

- *Status: Saving money*

### 7. Javascript - not functioning properly

Your resume webpage should include a visitor counter that displays how many people have accessed the site. You will need to write a bit of Javascript to make this happen. Here is a helpful tutorial to get you started in the right direction. Code adapted from: [How to Build Website visitor counter](https://contactmentor.com/build-website-visitor-counter-javascript/?expand_article=1)

Update file in: `/js/main.js`

```javascript
   /* Website Counter */
    var counterContainer = document.querySelector(".website-counter");
    var visitCount = localStorage.getItem("page_view");

    // Check if page_view entry is present
    if (visitCount) {
    visitCount = Number(visitCount) + 1;
    localStorage.setItem("page_view", visitCount);
    } else {
    visitCount = 1;
    localStorage.setItem("page_view", 1);
    }
    counterContainer.innerHTML = visitCount;
```

Update file in: `css/styles.css`

```css
/* ===================================================================
 * # Website counter
 *
 * ------------------------------------------------------------------- */

/* Styles for website counter container */
.website-counter {
  color: white;
  display: inline-block;

```

Update file in: `/index.html`

```html
<span>Visitor Counter</span>
<span class="website-counter"></span>
```

- *Status: Work in progress July 7, 2023. Using either `localStorage` or `sessionStorage` does not persist the cookies between different origins. Find a new solution.*

### 8. Database

The visitor counter will need to retrieve and update its count in a database somewhere. I suggest you use the Table API of Azure’s CosmosDB for this. (Use serverless capacity mode for the database and you’ll pay essentially nothing, unless you store or retrieve much more data than this project requires.)

- *Status: Not started.*

### 9. API

Do not communicate directly with CosmosDB from your Javascript code. Instead, you will need to create an API that accepts requests from your web app and communicates with the database. I suggest using Azure Functions with an HTTP trigger for this. They will be free or close to free for what we are doing.

- *Status: Not started.*

### 10. Python

You will need to write a bit of code in the Azure Function; you could use more Javascript, but it would be better for our purposes to explore Python – a common language used in back-end programs and scripts – and its Azure SDK. Here is a good, free Python tutorial.

- *Status: Not started.*

### 11. Tests

You should also include some tests for your Python code. Here are some resources on writing good Python tests.

- *Status: Not started.*

### 12. Infrastructure as Code

You should not be configuring your API resources – the Azure Function, the CosmosDB – manually, by clicking around in the Azure console. Instead, define them in an Azure Resource Manager (ARM) template on a Consumption plan. This is called “infrastructure as code” or IaC. It saves you time in the long run.

- *Status: Not started.*

### 13. Source Control

You do not want to be updating either your back-end API or your front-end website by making calls from your laptop, though. You want them to update automatically whenever you make a change to the code. (This is called continuous integration and deployment, or CI/CD.) Create a GitHub repository for your backend code.

- *Status: Not started.*

### 14. CI/CD (Back end)

Set up GitHub Actions such that when you push an update to your ARM template or Python code, your Python tests get run. If the tests pass, the ARM application should get packaged and deployed to Azure.

- *Status: Not started.*

### 15. CI/CD (Front end)

Create a second GitHub repository for your website code. Create GitHub Actions such that when you push new website code, the Azure Storage blob automatically gets updated. (You may need to purge your Azure CDN endpoint in the code as well.) Important note: DO NOT commit Azure credentials to source control! Bad hats will find them and use them against you!

- *Status: Not started.*

### 16. Blog post

Finally, in the text of your resume, you should link a short blog post describing some things you learned while working on this project. Dev.to or Hashnode are great places to publish if you don’t have your own blog.

And that’s the gist of it! For strategies, tools, and further challenges to help you get hired in cloud, check out the Azure edition of the Cloud Resume Challenge book.

- *Status: Not started.*
