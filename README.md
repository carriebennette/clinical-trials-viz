# Visualizing FDA approvals

I've been studying drug approvals and the pharmaceutical industry, with a focus on oncology, for years. I'd seen a few data visualizations summarizing the number of approvals over time, but none that grouped drugs by therapeutic class or visually encoded how many patients were included in the clinical trials supporting approval. I wanted to create a visualization of drug approals using a beeswarm plot, grouping by drug therapeutic class and having bubble size illustrate the number of patients studied to support each approval. You can see the the final visualization [here]( https://carriebennette.github.io/fda-approvals-viz/) and read more about its creation below.     

# Raw data preparation

## Scraping data from the web
I knew I wanted to include additional details about each approval (most notably the indication as well as the generic and brand name). Unfortunately the FDA database doesn't provide this information in a structured format. So I scraped these details from the [drugs.com website](https://www.drugs.com/newdrugs-archive/). The scrape_web_for_fda_approvals_data.R script scrapes all available data (approval from 2003-2019, although only approvals 2010-2019 are used in the final visualization).  

## Cross referencing data with the FDA approvals database
I still used the official Drugs@FDA database as the source of truth for FDA approval of New Molecular Entities. The FDA provides the underlying data files from this database for download [here](https://www.fda.gov/drugs/drug-approvals-and-databases/drugsfda-data-files). These are pretty straightforward files.  ***ADD BIT ABOUT CDER (no biologic products here!) ***

## Categorizing drugs using the Anatomical Therapeutic Chemical (ATC) Classification system
I used the Anatomical Therapeutic Chemical (ATC) classification system, which groups the active substances according to the to the organ or system on which they act and their therapeutic, pharmacological and chemical properties.  Finding a relatively clean dataset that included all ATC codes _and_ all CUI (Concept Unique Identifier) codes (used by SuppAI) was tricky (a bunch I discovered early were incomplete), but I eventually found a complete list as part of the [National Center for Biomedical Ontology](https://bioportal.bioontology.org/ontologies/ATC). I first discovered this resource when working on a prior visualization of supplement-drug interactions and was happy to get a chance to use it again. 

## Manually curating patient numbers from FDA labels
One data element I really wanted to visualize was the number of patients included in the clinical trials supporting approval, and I wanted the breakdown by treatment type (i.e., number of patients who recieved the experimental therapy, a placebo control, or an active comparator). I spent a few hours searching for such dataset online, but couldn't find a publicly available version. The closest I got was the [FDA trial snapshots](https://www.fda.gov/drugs/drug-approvals-and-databases/drug-trials-snapshots), but this resource didn't provide a breakdown by the treatment type and only was available for drugs approved in the last few years. So I resigned myself to curating this data manually from each of the drug labels available on the FDA website. Yes, this took many hours. I focused on curating data on the number of patients studied for efficacy (i.e., excluding any safety-only or pharmacokinetic studies). Occasionally the label didn't include the relevant data and I then reviewed the summary review. 

# Data visualization 

## Setting up the force simulation
Continuing my journey into really learning D3 I spent A LOT of time trying to understand the inner workings of the force simulations. 


