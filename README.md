## Text-Extraction
This python script downloads bills as pdfs and extracts text for textual-analysis.

## Motivation
A short description of the motivation behind the creation and maintenance of the project. This should explain **why** the project exists.

The goal is to quickly summarize information about the bills a particular legislator sponsored, such as which other legislators he or she cosponsors bills with and the topics they most often legislate on. This python script performs a search on the North Carolina Legislature's bill search website. The user provies keyword(s) to search on, such as a legislator's name, as well as the legislative session to search on (e.g., 2019-2020 session).

## Build status
Version 1

## How to use?
First, we use the selenium package to navigate to the search site. This form accepts a number of inputs, including key terms to search on as well as the session to filter by. Selenium navigates to these input boxes and dropdowns using xpaths to target the elements. Having filled these inputs, it clicks the Search button.

bill_search
![bill_search](https://github.com/[drussel4]/[Text-Extraction]/blob/master/[img]/[HowToUse]/bill_search.png?raw=true)

bill_search_filled_in

retrieveBills1

retrieveBills2

The results page gives us a list of bills that match the criteria we provided. Our code walks in and out of each bill's page, retrieving firstly the information (metadata) about the bill, such as bill number, bill name, and who sponsored it.

bill_search_results

Then it reads and downloads the PDF of the latest version of the bill, in official language. The raw text of the bill is later used for textual analysis.

retrieveBills3

bill_description_example

text_extractor

bill_text_example

Our code extracts text on a page-by-page basis and stores each as an element in a dict. It then concatenates all pages of a bill together for a single text object.

page_compiler

pdfExtractor

Having retrieved metadata and raw text for each bill, we generate three exhibits:
1. A wordcloud that showcases the frequency of terms in the raw text of every bill that was returned in the search results.
2. A bar chart displaying the frequency of sponsors on the bills returned in the search results. In this way we can see the legislators that collaborate most frequently with the legislator we searched on.
3. A bar chart displaying the frequency of key terms associated with the bills returned in the search results. In this way we can see the pursued by the legislator we searched on.

